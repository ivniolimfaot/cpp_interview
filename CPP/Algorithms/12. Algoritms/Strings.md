### 1. Algorithms & Data Structures (C++): Backspace String Compare

Backspace String Compare is a common algorithm problem where you're given two strings containing backspace characters ('#'). The task is to determine if the strings are equal after processing the backspace characters. When encountering a backspace character ('#'), you should remove the preceding character from the string. Here's a C++ implementation for this problem:

```cpp
#include <iostream>
#include <string>
using namespace std;

bool backspaceCompare(string S, string T) {
    int i = S.size() - 1, j = T.size() - 1;
    int skipS = 0, skipT = 0;

    while (i >= 0 || j >= 0) {
        while (i >= 0) {
            if (S[i] == '#') {
                skipS++;
                i--;
            } else if (skipS > 0) {
                skipS--;
                i--;
            } else {
                break;
            }
        }
        
        while (j >= 0) {
            if (T[j] == '#') {
                skipT++;
                j--;
            } else if (skipT > 0) {
                skipT--;
                j--;
            } else {
                break;
            }
        }
        
        if (i >= 0 && j >= 0 && S[i] != T[j]) {
            return false;
        }
        
        if ((i >= 0) != (j >= 0)) {
            return false;
        }
        
        i--;
        j--;
    }
    
    return true;
}

int main() {
    string S = "ab#c";
    string T = "ad#c";
    if (backspaceCompare(S, T)) {
        cout << "Strings are equal after processing backspaces.\n";
    } else {
        cout << "Strings are not equal after processing backspaces.\n";
    }
    return 0;
}
```

In this implementation, we use two pointers (`i` for string `S` and `j` for string `T`) to iterate through the strings in reverse order, simulating the effect of backspaces. We also use `skipS` and `skipT` variables to keep track of the number of consecutive backspaces encountered. We compare characters at the same index in both strings, ignoring characters removed due to backspaces. If at any point the characters don't match or the lengths of the two strings differ, we return `false`. Otherwise, if we successfully iterate through both strings without encountering any mismatches, we return `true`.

### 1. Algorithms & Data Structures (C++): Anagrams

To handle anagrams efficiently in C++, you can use a hashmap to store the frequency of characters in each word. Two words are anagrams if they have the same frequency of characters. Here's a sample implementation:

```cpp
#include <iostream>
#include <unordered_map>
#include <string>

// Function to check if two strings are anagrams
bool areAnagrams(const std::string& str1, const std::string& str2) {
    if (str1.length() != str2.length())
        return false;

    std::unordered_map<char, int> freqMap;

    // Count frequency of characters in str1
    for (char c : str1) {
        freqMap[c]++;
    }

    // Decrement frequency of characters in str2
    for (char c : str2) {
        if (freqMap.find(c) == freqMap.end() || freqMap[c] == 0)
            return false;
        freqMap[c]--;
    }

    return true;
}

int main() {
    std::string word1 = "listen";
    std::string word2 = "silent";
    
    if (areAnagrams(word1, word2)) {
        std::cout << word1 << " and " << word2 << " are anagrams.\n";
    } else {
        std::cout << word1 << " and " << word2 << " are not anagrams.\n";
    }

    return 0;
}
```

This program defines a function `areAnagrams` that takes two strings as input and returns true if they are anagrams, false otherwise. The function uses an unordered map (`std::unordered_map`) to store the frequency of characters in the first string. Then it iterates over the second string and decrements the frequency of each character found in the map. If the strings are anagrams, the map should be empty at the end of the process.

This implementation has a time complexity of O(n), where n is the length of the longer string, since it iterates over each character in both strings once.

### 1. Algorithms & Data Structures (C++): Anagrams in Substrings

To solve the problem of finding anagrams in substrings efficiently, you can use a sliding window approach combined with hashing. Here's a general outline of the algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

using namespace std;

vector<int> findAnagrams(string s, string p) {
    vector<int> result;
    if (s.empty() || p.empty() || s.length() < p.length()) {
        return result;
    }

    unordered_map<char, int> charCountP, charCountWindow;
    for (char c : p) {
        charCountP[c]++;
    }

    int windowSize = p.length();
    for (int i = 0; i < windowSize; ++i) {
        charCountWindow[s[i]]++;
    }

    if (charCountWindow == charCountP) {
        result.push_back(0);
    }

    for (int i = windowSize; i < s.length(); ++i) {
        charCountWindow[s[i - windowSize]]--;
        if (charCountWindow[s[i - windowSize]] == 0) {
            charCountWindow.erase(s[i - windowSize]);
        }
        charCountWindow[s[i]]++;

        if (charCountWindow == charCountP) {
            result.push_back(i - windowSize + 1);
        }
    }

    return result;
}

int main() {
    string s = "cbaebabacd";
    string p = "abc";
    vector<int> indices = findAnagrams(s, p);

    cout << "Anagram indices: ";
    for (int index : indices) {
        cout << index << " ";
    }
    cout << endl;

    return 0;
}
```

This algorithm maintains two hash maps: one for the characters in the pattern string `p` (`charCountP`), and one for the characters in the sliding window (`charCountWindow`). It iterates through the input string `s`, updating `charCountWindow` for each new character encountered.

The algorithm slides the window by removing the leftmost character and adding the rightmost character. At each step, it compares `charCountWindow` with `charCountP` to check if they are equal, indicating that an anagram of `p` is found in the current window.

The time complexity of this algorithm is O(n), where n is the length of the input string `s`, because we only iterate through `s` once. The space complexity is O(1) because the two hash maps (`charCountP` and `charCountWindow`) have a constant size (bounded by the number of unique characters in `p`).

### 1. Algorithms & Data Structures (C++): Anagrams in Substrings | Maps

To find all anagrams of a pattern within a string, you can use a sliding window approach combined with a hashmap (unordered_map in C++) to keep track of character frequencies. Here's how you can implement this in C++:

```cpp
#include <iostream>
#include <unordered_map>
#include <vector>
#include <string>

using namespace std;

vector<int> findAnagrams(string s, string p) {
    vector<int> result;
    if (s.empty() || p.empty() || s.size() < p.size())
        return result;

    unordered_map<char, int> targetMap, windowMap;
    for (char c : p) targetMap[c]++;

    int left = 0, right = 0, count = p.size();

    while (right < s.size()) {
        char currentChar = s[right];
        if (targetMap.find(currentChar) != targetMap.end()) {
            windowMap[currentChar]++;
            if (windowMap[currentChar] <= targetMap[currentChar])
                count--;
        }

        while (count == 0) {
            if (right - left + 1 == p.size())
                result.push_back(left);

            char leftChar = s[left];
            if (targetMap.find(leftChar) != targetMap.end()) {
                windowMap[leftChar]--;
                if (windowMap[leftChar] < targetMap[leftChar])
                    count++;
            }
            left++;
        }
        right++;
    }

    return result;
}

int main() {
    string s = "cbaebabacd";
    string p = "abc";

    vector<int> indices = findAnagrams(s, p);

    cout << "Anagram indices: ";
    for (int index : indices)
        cout << index << " ";
    cout << endl;

    return 0;
}
```

This code will output the starting indices of all substrings of s that are anagrams of p.

### 1. Algorithms & Data Structures (C++): Biggest Number String

To create a function in C++ that returns the biggest possible number string from a given array of non-negative integers, you can follow these steps:

1. Convert each integer in the array to a string.
2. Sort the array of strings in non-ascending order but with a custom comparison function that ensures the concatenated string is in decreasing order.
3. Concatenate all the strings to form the biggest number.
4. Handle edge cases, like an empty array.

Here's how you can implement it:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <string>

using namespace std;

// Custom comparator to sort strings in decreasing order when concatenated
bool customCompare(const string& a, const string& b) {
    return (a + b) > (b + a);
}

string largestNumber(vector<int>& nums) {
    // Convert each integer to a string
    vector<string> numStrs;
    for (int num : nums) {
        numStrs.push_back(to_string(num));
    }
    
    // Sort the strings using custom comparator
    sort(numStrs.begin(), numStrs.end(), customCompare);
    
    // Handle edge case when all numbers are 0
    if (numStrs[0] == "0") return "0";
    
    // Concatenate sorted strings
    string result;
    for (const string& numStr : numStrs) {
        result += numStr;
    }
    
    return result;
}

int main() {
    // Example usage
    vector<int> nums = {3, 30, 34, 5, 9};
    cout << "The biggest number string: " << largestNumber(nums) << endl;
    
    return 0;
}
```

This code defines a custom comparator `customCompare` which is used in sorting the array of strings. This comparator ensures that when two strings are concatenated, they are in decreasing order. The `largestNumber` function handles the conversion, sorting, and concatenation. Finally, the `main` function demonstrates the usage of the `largestNumber` function with an example array of integers.

### 1. Algorithms & Data Structures (C++): Binary String to Number

Converting a binary string to a number in C++ is a fundamental operation. You can achieve this using a simple algorithm by iterating through each character of the string, starting from the most significant digit (leftmost) to the least significant digit (rightmost), and accumulating the result.

Here's a basic implementation:

```cpp
#include <iostream>
#include <string>
using namespace std;

int binaryStringToNumber(const string& binary) {
    int result = 0;
    for (char bit : binary) {
        // Multiply the result by 2 and add the current bit (0 or 1)
        result = (result << 1) + (bit - '0');
    }
    return result;
}

int main() {
    string binary = "101010"; // Example binary string
    int number = binaryStringToNumber(binary);
    cout << "Binary: " << binary << endl;
    cout << "Number: " << number << endl;
    return 0;
}
```

Explanation:

1. We define a function `binaryStringToNumber` that takes a binary string as input and returns the corresponding decimal number.
2. We initialize `result` to 0, which will accumulate the decimal value.
3. We iterate through each character of the binary string.
4. For each bit, we shift the current result left by 1 bit (`result << 1`) to make room for the new bit and then add the value of the current bit (`bit - '0'`).
5. Finally, we return the accumulated result.

In the `main()` function, we demonstrate the usage by converting a binary string `"101010"` to its corresponding decimal number. You can replace `"101010"` with any other binary string you want to convert.

### 1. Algorithms & Data Structures (C++): Binary Strings

Binary strings are sequences of characters that consist only of '0's and '1's. In C++, you can represent binary strings using the `std::string` class or simply using character arrays (`char[]`). Here's a simple C++ code demonstrating basic operations on binary strings:

```cpp
#include <iostream>
#include <string>

// Function to check if a string is a valid binary string
bool isValidBinaryString(const std::string& str) {
    for (char c : str) {
        if (c != '0' && c != '1') {
            return false;
        }
    }
    return true;
}

// Function to count the number of set bits (number of '1's) in a binary string
int countSetBits(const std::string& str) {
    int count = 0;
    for (char c : str) {
        if (c == '1') {
            count++;
        }
    }
    return count;
}

int main() {
    std::string binaryStr = "1010101";

    // Check if the string is a valid binary string
    if (isValidBinaryString(binaryStr)) {
        std::cout << "The string is a valid binary string." << std::endl;

        // Count the number of set bits
        int numSetBits = countSetBits(binaryStr);
        std::cout << "Number of set bits: " << numSetBits << std::endl;
    } else {
        std::cout << "The string is not a valid binary string." << std::endl;
    }

    return 0;
}
```

This code defines two functions:

1. `isValidBinaryString`: Checks if a given string is a valid binary string.
2. `countSetBits`: Counts the number of set bits (number of '1's) in a binary string.

In the `main` function, we demonstrate the usage of these functions by checking if a binary string is valid and then counting the number of set bits in it. You can modify and extend this code according to your requirements for more complex operations on binary strings.

### 1. Algorithms & Data Structures (C++): Brute Force Matcher

A Brute Force Matcher is a simple algorithm used for pattern matching in strings. It's not the most efficient approach, but it's straightforward and works well for small datasets or when other more complex algorithms might be overkill. Here's a basic implementation in C++:

```cpp
#include <iostream>
#include <string>

using namespace std;

// Function to perform brute force pattern matching
void bruteForceMatcher(const string& text, const string& pattern) {
    int n = text.length();
    int m = pattern.length();

    // Iterate through text
    for (int i = 0; i <= n - m; ++i) {
        int j;

        // Check if pattern matches starting at position i in text
        for (j = 0; j < m; ++j) {
            if (text[i + j] != pattern[j])
                break;
        }

        // If the inner loop completed without breaking, pattern found at position i
        if (j == m)
            cout << "Pattern found at index " << i << endl;
    }
}

int main() {
    string text = "a quick brown fox jumps over the lazy dog";
    string pattern = "fox";

    cout << "Text: " << text << endl;
    cout << "Pattern: " << pattern << endl;

    bruteForceMatcher(text, pattern);

    return 0;
}
```

This program demonstrates a simple brute force pattern matching algorithm. It iterates through the text and checks if the pattern matches at each position. If a match is found, it prints the index where the pattern starts in the text.

Keep in mind that the time complexity of this algorithm is O((n-m+1)*m), where n is the length of the text and m is the length of the pattern. This means it's not very efficient for large datasets or patterns, as the time it takes to find a match grows with both the length of the text and the pattern.

### 1. Algorithms & Data Structures (C++): Brute Force Pattern Matching using STL

Brute force pattern matching is a simple but inefficient algorithm for finding occurrences of a pattern within a text. In C++, you can implement it using the Standard Template Library (STL) string and vector classes. Here's a basic example of how you can do it:

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

vector<int> bruteForcePatternMatch(const string& text, const string& pattern) {
    vector<int> matches;

    // Loop through the text
    for (int i = 0; i <= text.length() - pattern.length(); ++i) {
        bool found = true;

        // Check if the pattern matches starting at position i
        for (int j = 0; j < pattern.length(); ++j) {
            if (text[i + j] != pattern[j]) {
                found = false;
                break;
            }
        }

        // If the pattern is found, add the starting index to the matches vector
        if (found) {
            matches.push_back(i);
        }
    }

    return matches;
}

int main() {
    string text = "abracadabra";
    string pattern = "abra";

    vector<int> matches = bruteForcePatternMatch(text, pattern);

    if (matches.empty()) {
        cout << "Pattern not found." << endl;
    } else {
        cout << "Pattern found at positions: ";
        for (int i = 0; i < matches.size(); ++i) {
            cout << matches[i] << " ";
        }
        cout << endl;
    }

    return 0;
}
```

This code defines a function `bruteForcePatternMatch` that takes two string arguments: `text` and `pattern`. It iterates through the text, checking for matches of the pattern at each position. If a match is found, the index where the match starts is added to a vector called `matches`. Finally, the `main` function demonstrates the usage of this algorithm by searching for the pattern "abra" within the text "abracadabra" and printing the positions where the pattern occurs.

### 1. Algorithms & Data Structures (C++): Changing Case of a String

To change the case of a string in C++, you can iterate through each character of the string and use the `tolower()` or `toupper()` functions from the `<cctype>` header to convert each character to lowercase or uppercase respectively. Here's a simple example:

```cpp
#include <iostream>
#include <string>
#include <cctype>

std::string toLowerCase(const std::string& str) {
    std::string result;
    for (char c : str) {
        result += std::tolower(c);
    }
    return result;
}

std::string toUpperCase(const std::string& str) {
    std::string result;
    for (char c : str) {
        result += std::toupper(c);
    }
    return result;
}

int main() {
    std::string input = "Hello World";
    std::string lowerCaseStr = toLowerCase(input);
    std::string upperCaseStr = toUpperCase(input);
    
    std::cout << "Original string: " << input << std::endl;
    std::cout << "Lowercase: " << lowerCaseStr << std::endl;
    std::cout << "Uppercase: " << upperCaseStr << std::endl;
    
    return 0;
}
```

In this example, the `toLowerCase()` function converts each character of the input string to lowercase, and the `toUpperCase()` function converts each character to uppercase. Then, we demonstrate these functions in the `main()` function.

### 1. Algorithms & Data Structures (C++): Character Array: cin.getline()

In C++, `cin.getline()` is a function used to read a line of text from the standard input (usually the keyboard) and store it in a character array (string). It's particularly useful when you want to read input containing spaces or newline characters. Here's how it works:

```cpp
#include <iostream>

int main() {
    const int maxLength = 100; // maximum length of input
    char input[maxLength]; // character array to store input
    
    std::cout << "Enter a sentence: ";
    
    // Read input using cin.getline()
    std::cin.getline(input, maxLength);
    
    // Display the input
    std::cout << "You entered: " << input << std::endl;
    
    return 0;
}
```

In the code above:

- We include the `<iostream>` header for input and output operations.
- We declare a character array `input` of size `maxLength` to store the input.
- We prompt the user to enter a sentence.
- We use `cin.getline(input, maxLength)` to read a line of input from the standard input into the `input` array. It takes two parameters: the array to store the input and the maximum number of characters to read (including the null character).
- Finally, we display the input back to the user.

One key difference between `cin.getline()` and `cin >>` is that `cin.getline()` reads until it encounters a newline character (`'\n'`) or reaches the maximum number of characters specified, whereas `cin >>` reads until it encounters whitespace (space, tab, newline).

### 1. Algorithms & Data Structures (C++): Character Array: Inbuilt functions

In C++, character arrays are often manipulated using a variety of inbuilt functions from the standard library. Here are some common functions used for working with character arrays:

1. **strlen()**: This function is used to find the length of a string. It returns the number of characters in the string excluding the null character '\0'.

```cpp
#include <cstring>

char str[] = "Hello";
int length = strlen(str); // length will be 5
```

1. **strcpy()**: This function is used to copy one string to another. It copies the entire string including the null character.

```cpp
#include <cstring>

char source[] = "Hello";
char destination[20];
strcpy(destination, source); // destination will contain "Hello\0"
```

1. **strcat()**: This function is used to concatenate two strings. It appends a copy of the source string to the destination string.

```cpp
#include <cstring>

char str1[20] = "Hello";
char str2[] = " World";
strcat(str1, str2); // str1 will contain "Hello World\0"
```

1. **strcmp()**: This function is used to compare two strings. It returns an integer less than, equal to, or greater than zero if the first string is found, respectively, to be less than, to match, or be greater than the second string.

```cpp
#include <cstring>

char str1[] = "apple";
char str2[] = "banana";
int result = strcmp(str1, str2); // result will be negative since "apple" comes before "banana" in lexicographical order
```

1. **strchr()**: This function is used to find the first occurrence of a character in a string. It returns a pointer to the first occurrence of the character, or NULL if the character is not found.

```cpp
#include <cstring>

char str[] = "Hello";
char *ptr = strchr(str, 'l'); // ptr will point to the first 'l' in "Hello"
```

1. **strstr()**: This function is used to find the first occurrence of a substring within a string. It returns a pointer to the first occurrence of the substring, or NULL if the substring is not found.

```cpp
#include <cstring>

char str[] = "Hello World";
char *ptr = strstr(str, "World"); // ptr will point to "World" within "Hello World"
```

These are some of the most commonly used functions for manipulating character arrays in C++. They provide powerful tools for working with strings efficiently.

### 1. Algorithms & Data Structures (C++): Character Array: Length of String

In C++, a character array representing a string ends with a null character `\0`. You can find the length of the string by iterating through the array until you encounter the null character. Here's a simple example:

```cpp
#include <iostream>

// Function to find the length of a string
int stringLength(const char* str) {
    int length = 0;
    // Iterate until null character is found
    while (str[length] != '\0') {
        length++;
    }
    return length;
}

int main() {
    // Example string
    const char str[] = "Hello, world!";
    
    // Find the length of the string
    int length = stringLength(str);
    
    std::cout << "Length of the string: " << length << std::endl;
    
    return 0;
}
```

This program will output:

```bash
Length of the string: 13
```

Here, `stringLength()` function iterates through the character array `str` until it encounters the null character `\0`, counting each character encountered along the way. Once the null character is found, the function returns the count, which is the length of the string.

### 1. Algorithms & Data Structures (C++): Character Array: Print all prefixes

Sure, to print all the prefixes of a character array in C++, you can iterate through the array and print the substrings from index 0 to i for each i from 0 to the length of the array. Here's how you can implement it:

```cpp
#include <iostream>
#include <cstring>

using namespace std;

void printPrefixes(char arr[]) {
    int n = strlen(arr);
    for (int i = 0; i < n; i++) {
        for (int j = 0; j <= i; j++) {
            cout << arr[j];
        }
        cout << endl;
    }
}

int main() {
    char arr[] = "hello";
    printPrefixes(arr);
    return 0;
}
```

In this code:

- `printPrefixes` function takes a character array as input.
- It iterates through each character of the array.
- For each character, it prints the substring from index 0 to the current index.
- The main function demonstrates how to use this function with an example array "hello".

### 1. Algorithms & Data Structures (C++): Character Array: Reverse string

Sure! Here's a simple C++ function to reverse a character array (string):

```cpp
#include <iostream>

void reverseString(char str[]) {
    int length = 0;
    // Calculate the length of the string
    while (str[length] != '\0') {
        length++;
    }

    // Swap characters from start and end
    for (int i = 0; i < length / 2; i++) {
        char temp = str[i];
        str[i] = str[length - i - 1];
        str[length - i - 1] = temp;
    }
}

int main() {
    char str[] = "Hello, World!";
    
    std::cout << "Original string: " << str << std::endl;
    
    reverseString(str);
    
    std::cout << "Reversed string: " << str << std::endl;
    
    return 0;
}
```

This program will reverse the string "Hello, World!" and output "dlroW ,olleH".

### 1. Algorithms & Data Structures (C++): Character Arrays/Strings

Character arrays, often referred to as strings, are fundamental data structures used in C++ to store sequences of characters. Here's a basic overview of working with character arrays/strings in C++:

#### Declaration and Initialization

You can declare and initialize a character array in various ways:

```cpp
// Method 1: Declare with a fixed size
char str1[20]; // declares a character array of size 20

// Method 2: Declare and initialize with a string literal
char str2[] = "Hello";

// Method 3: Declare and initialize using strcpy (string copy)
char str3[20];
strcpy(str3, "World");

// Method 4: Declare and initialize using string constructor (C++ string class)
#include <string>
std::string str4 = "Hello";
```

#### Accessing Elements

You can access individual characters in a character array using array indexing:

```cpp
char str[] = "Hello";
char firstChar = str[0]; // 'H'
char secondChar = str[1]; // 'e'
```

#### Manipulating Strings

C++ provides several functions in the `<cstring>` header for string manipulation:

- `strlen(str)`: Returns the length of the string.
- `strcpy(dest, src)`: Copies the string `src` to `dest`.
- `strcat(dest, src)`: Concatenates `src` to the end of `dest`.
- `strcmp(str1, str2)`: Compares two strings. Returns 0 if equal, positive value if `str1` is greater, negative value if `str2` is greater.
- `strchr(str, ch)`: Returns a pointer to the first occurrence of `ch` in `str`, or NULL if not found.
- `strstr(str1, str2)`: Returns a pointer to the first occurrence of `str2` in `str1`, or NULL if not found.

#### C++ String Class

In addition to character arrays, C++ also provides a `string` class in the `<string>` header, which simplifies string manipulation:

```cpp
#include <string>
std::string str = "Hello";
std::string substr = str.substr(1, 3); // "ell"
str.append(" World"); // "Hello World"
```

#### Important Considerations

- Character arrays in C++ are null-terminated, meaning they end with a null character `'\0'`.
- Be cautious about buffer overflows when manipulating character arrays. Always ensure sufficient space to accommodate the data.
- C++ `string` class provides more safety and convenience compared to traditional character arrays, especially when dealing with dynamic memory allocation and manipulation.

Understanding character arrays/strings is crucial for handling text data efficiently in C++.

### 1. Algorithms & Data Structures (C++): Checking if 2 Strings are Anagram (distinct letters)

To check if two strings are anagrams (composed of the same letters), you need to compare if they contain the same characters with the same frequencies. Here's a C++ implementation using an algorithm based on counting the occurrences of each character:

```cpp
#include <iostream>
#include <string>
#include <unordered_map>

bool areAnagrams(const std::string& s1, const std::string& s2) {
    // If the lengths are different, they can't be anagrams
    if (s1.length() != s2.length()) {
        return false;
    }

    // Count occurrences of characters in the first string
    std::unordered_map<char, int> charCount;
    for (char c : s1) {
        charCount[c]++;
    }

    // Subtract occurrences of characters in the second string
    // If any character count goes negative or a character is missing, return false
    for (char c : s2) {
        if (charCount.find(c) == charCount.end() || --charCount[c] < 0) {
            return false;
        }
    }

    // If all characters matched and no extras, they are anagrams
    return true;
}

int main() {
    std::string str1, str2;
    std::cout << "Enter first string: ";
    std::cin >> str1;
    std::cout << "Enter second string: ";
    std::cin >> str2;

    if (areAnagrams(str1, str2)) {
        std::cout << "The strings are anagrams." << std::endl;
    } else {
        std::cout << "The strings are not anagrams." << std::endl;
    }

    return 0;
}
```

This code first counts the occurrences of each character in the first string, then it decrements those counts for each character in the second string. If at any point the count goes negative or if a character from the second string is not found in the first string, it returns `false`. Otherwise, it returns `true` indicating that the strings are anagrams.

### 1. Algorithms & Data Structures (C++): Comparing Strings and Checking Palindrome

Certainly! Here's an example of how you can compare strings and check for palindromes in C++:

```cpp
#include <iostream>
#include <string>
#include <algorithm>

// Function to compare two strings
bool compareStrings(const std::string& str1, const std::string& str2) {
    return str1 == str2;
}

// Function to check if a string is a palindrome
bool isPalindrome(const std::string& str) {
    std::string reversed = str;
    std::reverse(reversed.begin(), reversed.end());
    return str == reversed;
}

int main() {
    std::string str1 = "hello";
    std::string str2 = "world";
    
    // Comparing two strings
    if(compareStrings(str1, str2)) {
        std::cout << "The strings are equal.\n";
    } else {
        std::cout << "The strings are not equal.\n";
    }
    
    std::string palindrome = "racecar";
    
    // Checking if a string is a palindrome
    if(isPalindrome(palindrome)) {
        std::cout << "The string is a palindrome.\n";
    } else {
        std::cout << "The string is not a palindrome.\n";
    }
    
    return 0;
}
```

In this code:

- The `compareStrings` function compares two strings using the `==` operator.
- The `isPalindrome` function checks if a given string is a palindrome by comparing it with its reversed version using `std::reverse`.
- In the `main` function, we demonstrate the usage of these functions by comparing two strings and checking if a string is a palindrome.

### 1. Algorithms & Data Structures (C++): Convert one string to another

To convert one string to another using C++, you can employ various algorithms and techniques, such as dynamic programming. One popular algorithm for this task is the Levenshtein distance algorithm, which calculates the minimum number of single-character edits (insertions, deletions, or substitutions) required to change one string into another. Here's a basic implementation of the Levenshtein distance algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int minDistance(string word1, string word2) {
    int m = word1.length();
    int n = word2.length();
    
    // Create a 2D vector to store the distances
    vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));
    
    // Initialize the first row and column
    for (int i = 0; i <= m; ++i) {
        dp[i][0] = i;
    }
    for (int j = 0; j <= n; ++j) {
        dp[0][j] = j;
    }
    
    // Fill in the rest of the matrix
    for (int i = 1; i <= m; ++i) {
        for (int j = 1; j <= n; ++j) {
            if (word1[i - 1] == word2[j - 1]) {
                dp[i][j] = dp[i - 1][j - 1];
            } else {
                dp[i][j] = 1 + min({dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]});
            }
        }
    }
    
    // The bottom-right cell contains the Levenshtein distance
    return dp[m][n];
}

int main() {
    string word1 = "kitten";
    string word2 = "sitting";
    
    int distance = minDistance(word1, word2);
    cout << "Minimum number of edits to convert \"" << word1 << "\" to \"" << word2 << "\": " << distance << endl;
    
    return 0;
}
```

This code defines a function `minDistance` that calculates the minimum number of edits required to convert `word1` to `word2`. In the `main` function, you can specify the two strings you want to convert. This implementation uses dynamic programming to efficiently compute the Levenshtein distance.

### 1. Algorithms & Data Structures (C++): Convert one string to another using Dynamic Programming

Sure! You can use Dynamic Programming to convert one string to another efficiently. One common algorithm to achieve this is the Wagner-Fischer algorithm, also known as the Edit Distance algorithm. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>

using namespace std;

int minDistance(string word1, string word2) {
    int m = word1.length();
    int n = word2.length();

    // Create a 2D vector to store the dynamic programming table
    vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));

    // Fill in the base cases
    for (int i = 0; i <= m; ++i) {
        dp[i][0] = i;
    }
    for (int j = 0; j <= n; ++j) {
        dp[0][j] = j;
    }

    // Fill in the rest of the table
    for (int i = 1; i <= m; ++i) {
        for (int j = 1; j <= n; ++j) {
            if (word1[i - 1] == word2[j - 1]) {
                dp[i][j] = dp[i - 1][j - 1];
            } else {
                dp[i][j] = 1 + min({dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]});
            }
        }
    }

    // The bottom-right cell of the dp table contains the minimum number of operations required
    return dp[m][n];
}

int main() {
    string word1 = "kitten";
    string word2 = "sitting";

    int distance = minDistance(word1, word2);

    cout << "Minimum operations required: " << distance << endl;

    return 0;
}
```

This code calculates the minimum number of operations (insertions, deletions, or substitutions) required to convert `word1` into `word2`. The time complexity of this algorithm is O(m*n), where m and n are the lengths of the input strings `word1` and `word2` respectively.

### 1. Algorithms & Data Structures (C++): Convert String to Integer

Converting a string to an integer in C++ is a common task. Here's a simple implementation using standard library functions:

```cpp
#include <iostream>
#include <string>
#include <sstream>

int stringToInt(const std::string& s) {
    std::stringstream ss(s);
    int result;
    ss >> result;
    return result;
}

int main() {
    std::string str = "12345";
    int num = stringToInt(str);
    std::cout << "Converted integer: " << num << std::endl;
    return 0;
}
```

In this example:

- `stringToInt` function takes a `std::string` as input.
- It creates a `std::stringstream` object `ss` and initializes it with the input string `s`.
- It then extracts an integer from the stringstream using the `>>` operator into the `result` variable.
- Finally, it returns the converted integer.

Remember to include necessary header files (`

iostream`, `string`, and `sstream`) at the beginning of your program. This implementation assumes that the input string contains a valid integer representation. If the string contains non-integer characters or exceeds the range of integer values, additional error handling may be required.

### 1. Algorithms & Data Structures (C++): Convert String using Bottom Up

Sure, converting a string using a bottom-up approach typically involves dynamic programming. The idea is to break down the problem into smaller subproblems and solve them iteratively, building up to the final solution. Here's an example in C++:

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <unordered_set>

using namespace std;

string convertString(const string& s, const unordered_set<string>& dictionary) {
    int n = s.length();
    vector<string> dp(n + 1, "");
    
    for (int i = n - 1; i >= 0; --i) {
        string current;
        for (int j = i; j < n; ++j) {
            current += s[j];
            if (dictionary.find(current) != dictionary.end()) {
                if (!dp[i].empty()) {
                    dp[i] = (dp[i] + " " + current);
                } else {
                    dp[i] = current;
                }
            }
        }
    }
    
    return dp[0];
}

int main() {
    string s = "applepie";
    unordered_set<string> dictionary = {"apple", "pie", "peach", "pier", "applepie"};
    
    string result = convertString(s, dictionary);
    cout << "Converted string: " << result << endl;
    
    return 0;
}
```

In this code:

- `convertString` takes a string `s` and a set of words `dictionary`.
- It initializes a dynamic programming table `dp` where `dp[i]` will store the converted string starting from index `i` to the end of the input string.
- It iterates through each character of the input string `s`, starting from the end, and builds the converted string bottom-up.
- At each position, it checks all possible substrings from that position to the end and if any substring is found in the dictionary, it updates the `dp` table accordingly.
- Finally, it returns the converted string starting from the beginning of the input string.

You can modify the main function to use your own input string and dictionary.

### 1. Algorithms & Data Structures (C++): Count sorted vowel strings

Counting sorted vowel strings is a classic problem in computer science that involves finding the number of strings consisting of lowercase vowels (a, e, i, o, u) that are sorted lexicographically.

Here's a C++ implementation to count the number of sorted vowel strings of length `n`:

```cpp
#include <iostream>
using namespace std;

int countSortedVowelStrings(int n) {
    // Initialize counts for each vowel
    int a = 1, e = 1, i = 1, o = 1, u = 1;

    for (int j = 2; j <= n; ++j) {
        // Update counts for each vowel based on previous counts
        a = a + e + i + o + u; // 'a' can follow any vowel
        e = e + i + o + u;     // 'e' can follow 'a', 'e', 'i', 'o', or 'u'
        i = i + o + u;         // 'i' can follow 'e', 'i', 'o', or 'u'
        o = o + u;             // 'o' can follow 'i', 'o', or 'u'
        u = u;                 // 'u' can only follow 'u'
    }

    // Total count is the sum of counts of all vowels
    return a + e + i + o + u;
}

int main() {
    int n;
    cout << "Enter the length of the string: ";
    cin >> n;
    cout << "Number of sorted vowel strings of length " << n << ": " << countSortedVowelStrings(n) << endl;
    return 0;
}
```

This code defines a function `countSortedVowelStrings` that takes an integer `n` as input, representing the length of the string. The function calculates the count of sorted vowel strings of length `n` using dynamic programming. Finally, the `main` function takes user input for the length of the string and prints the result.

For example, if the input is `n = 2`, the output would be `Number of sorted vowel strings of length 2: 15`, as there are 15 sorted vowel strings of length 2.

### 1. Algorithms & Data Structures (C++): Count sorted vowel strings (problem)

The problem of counting sorted vowel strings can be approached in various ways using algorithms and data structures in C++. One approach is to use dynamic programming to count the number of strings of a given length that consist only of vowels (a, e, i, o, u) and are in sorted order.

Here's a C++ solution using dynamic programming:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int countSortedVowelStrings(int n) {
    // Create a 2D DP array to store the counts
    vector<vector<int>> dp(n + 1, vector<int>(5, 0));
    
    // Base case: for n = 1, there is one string of each vowel
    for (int i = 0; i < 5; ++i) {
        dp[1][i] = 1;
    }
    
    // Fill the DP table
    for (int i = 2; i <= n; ++i) {
        for (int j = 0; j < 5; ++j) {
            // For each vowel, the count is the sum of counts of smaller length strings
            for (int k = 0; k <= j; ++k) {
                dp[i][j] += dp[i - 1][k];
            }
        }
    }
    
    // Sum up counts for all vowels at length n
    int count = 0;
    for (int i = 0; i < 5; ++i) {
        count += dp[n][i];
    }
    
    return count;
}

int main() {
    int n;
    cout << "Enter the length of strings: ";
    cin >> n;
    
    cout << "Number of sorted vowel strings of length " << n << ": " << countSortedVowelStrings(n) << endl;
    
    return 0;
}
```

In this solution, we use a 2D vector `dp` to store the counts of strings of length `n` ending with each vowel. We initialize the base case for `n=1`, and then iterate through each length, updating the counts based on previous lengths. Finally, we sum up the counts for all vowels at length `n` to get the total count of sorted vowel strings of length `n`.

You can run this code and input the desired length of strings to get the count of sorted vowel strings of that length.

### 1. Algorithms & Data Structures (C++): Count sorted vowel strings (solution)

To count the number of sorted strings containing only vowels (a, e, i, o, u) of length n in C++, you can use dynamic programming. Here's a solution using dynamic programming:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int countSortedVowelStrings(int n) {
    // Initialize a 2D vector to store counts of strings ending with each vowel
    vector<vector<int>> dp(n + 1, vector<int>(5, 0));

    // Initialize counts for strings of length 1
    for (int i = 0; i < 5; ++i)
        dp[1][i] = 1;

    // Compute counts for strings of length > 1
    for (int i = 2; i <= n; ++i) {
        for (int j = 0; j < 5; ++j) {
            // For each vowel j, count strings ending with vowel j
            // by summing counts of strings ending with vowels <= j in previous positions
            for (int k = 0; k <= j; ++k) {
                dp[i][j] += dp[i - 1][k];
            }
        }
    }

    // Sum counts of strings of length n
    int count = 0;
    for (int i = 0; i < 5; ++i) {
        count += dp[n][i];
    }

    return count;
}

int main() {
    int n;
    cout << "Enter the length of the string: ";
    cin >> n;

    cout << "Number of sorted vowel strings of length " << n << ": " << countSortedVowelStrings(n) << endl;

    return 0;
}
```

This code defines a function `countSortedVowelStrings` that takes an integer `n` as input and returns the number of sorted strings containing only vowels of length `n`. It uses dynamic programming to compute the counts efficiently. The main function prompts the user to enter the length of the string and then prints the result.

### 1. Algorithms & Data Structures (C++): Count sorted vowel strings: Complexity analysis

To analyze the complexity of the algorithm for counting sorted vowel strings in C++, let's first understand the problem and then analyze the solution.

**Problem Statement:**
Given an integer `n`, we need to count all possible strings of length `n` that consists of vowels (a, e, i, o, u) and are sorted lexicographically.

**Algorithm:**

The algorithm to solve this problem typically involves dynamic programming. Here's a brief outline:

1. Initialize a 2D array `dp` of size `(n + 1) x 5`, where `dp[i][j]` represents the count of valid strings of length `i` ending with vowel `j` (0 for 'a', 1 for 'e', and so on).
2. Initialize the base cases: `dp[1][j] = 1` for all `j`.
3. For each length from `2` to `n`:
   - For each vowel `j`, calculate `dp[i][j]` as the sum of `dp[i-1][k]` for all `k` such that `k <= j`.
4. Sum up the counts in the last row of the `dp` array to get the total count of valid strings of length `n`.

**Complexity Analysis:**

Let's denote:

- `n` as the length of the string.
- `V = 5` as the number of vowels.

1. **Space Complexity:**
   - We use a 2D array of size `(n + 1) x 5` for dynamic programming. So, the space complexity is `O(n)`.

2. **Time Complexity:**
   - Initializing the DP array takes `O(n)` time.
   - Calculating each entry of the DP array takes constant time, as it involves only a constant number of operations.
   - So, the time complexity of the DP approach is `O(n)`.

Overall, the time complexity of the algorithm is `O(n)` and the space complexity is also `O(n)`. This makes the algorithm efficient for counting sorted vowel strings for large values of `n`.

### 1. Algorithms & Data Structures (C++): Count Strings

Sure, let's discuss a common algorithm problem: counting strings.

**Problem Statement:**

Given a set of strings, we want to count the number of strings that meet a certain condition. For example, let's say we have a set of strings and we want to count how many of them start with a particular letter.

**Example:**

Let's consider a set of strings: {"apple", "banana", "apricot", "grape", "orange"}. We want to count how many strings start with the letter 'a'. In this case, the answer would be 2 because "apple" and "apricot" start with 'a'.

**Approach:**

One common approach to solve this problem is to iterate through each string in the set and check if it meets the condition. If it does, we increment our count.

Here's a simple algorithm in C++ to count the number of strings that start with a given character:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

int countStringsStartingWith(const vector<string>& strings, char startChar) {
    int count = 0;
    for (const string& str : strings) {
        if (str.front() == startChar) {
            count++;
        }
    }
    return count;
}

int main() {
    vector<string> strings = {"apple", "banana", "apricot", "grape", "orange"};
    char startChar = 'a';
    int count = countStringsStartingWith(strings, startChar);
    cout << "Number of strings starting with '" << startChar << "': " << count << endl;
    return 0;
}
```

In this code:

- The `countStringsStartingWith` function takes a vector of strings and a character as input.
- It iterates through each string in the vector and checks if the first character of the string matches the given character.
- If a match is found, it increments the count.
- Finally, it returns the count.

This is a basic example, but you can modify the condition inside the loop to check for any other criteria you need.

### 1. Algorithms & Data Structures (C++): Counting Subsequences

Certainly! Counting subsequences is a common problem in algorithms and data structures. A subsequence of a string is a sequence that can be derived from the original string by deleting zero or more characters without changing the relative order of the remaining characters.

Here's a simple approach in C++ to count the number of subsequences of a given string:

```cpp
#include <iostream>
#include <cstring>

// Function to count subsequences
int countSubsequences(const char* str) {
    int n = strlen(str);
    
    // Array to store counts of subsequences ending with different characters
    int dp[26] = {0}; // Assuming input string contains only lowercase English alphabets
    
    for (int i = 0; i < n; i++) {
        // Increment count of subsequences ending with the current character
        dp[str[i] - 'a']++;
        
        // Add counts of subsequences ending with all previous characters
        for (int j = 0; j < 26; j++) {
            if (j != str[i] - 'a') {
                dp[str[i] - 'a'] += dp[j];
            }
        }
    }
    
    // Sum up counts of all subsequences
    int count = 0;
    for (int i = 0; i < 26; i++) {
        count += dp[i];
    }
    
    return count;
}

int main() {
    const char* str = "abc";
    std::cout << "Number of subsequences: " << countSubsequences(str) << std::endl;
    return 0;
}
```

This code first initializes an array `dp` to store counts of subsequences ending with different characters. Then, it iterates through the input string, updating the counts of subsequences at each step. Finally, it sums up the counts of all subsequences to get the total number of subsequences.

You can replace the `const char* str = "abc";` line in the `main` function with any string you want to count the subsequences for.

### 1. Algorithms & Data Structures (C++): Counting Subsequences - Bottom Up

Sure, let's dive into a C++ implementation of counting subsequences using bottom-up dynamic programming. Here's a simple example:

```cpp
#include <iostream>
#include <vector>
using namespace std;

int countSubsequences(const string& s, const string& t) {
    int m = s.size();
    int n = t.size();

    // Create a 2D table to store the counts of subsequences
    vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));

    // Initialize the first row with 1s as an empty string is a subsequence of any string
    for (int i = 0; i <= m; ++i)
        dp[i][0] = 1;

    // Fill the dp table bottom-up
    for (int i = 1; i <= m; ++i) {
        for (int j = 1; j <= n; ++j) {
            if (s[i - 1] == t[j - 1])
                // If the characters match, we can include this character in the subsequence
                dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j];
            else
                // If the characters don't match, we can't include this character
                dp[i][j] = dp[i - 1][j];
        }
    }

    // The bottom-right cell contains the count of subsequences
    return dp[m][n];
}

int main() {
    string s = "abcabc";
    string t = "abc";
    cout << "Count of subsequences: " << countSubsequences(s, t) << endl;
    return 0;
}
```

In this implementation, we're using a 2D vector `dp` to store the counts of subsequences. The cell `dp[i][j]` represents the count of subsequences of the substring `s[0...i-1]` that match the substring `t[0...j-1]`.

We initialize the first row of `dp` with 1s because an empty string is a subsequence of any string. Then, we iterate over each character of `s` and `t`, updating the counts based on whether the characters match or not.

Finally, the value in `dp[m][n]` (where `m` and `n` are the lengths of `s` and `t` respectively) represents the count of subsequences of `s` that match `t`.

### 1. Algorithms & Data Structures (C++): Counting Subsequences - Table Filling

Counting subsequences efficiently often involves dynamic programming techniques. One common approach is using a table filling method. Here's a C++ implementation of counting subsequences using table filling:

```cpp
#include <iostream>
#include <vector>

int countSubsequences(const std::string& s, const std::string& t) {
    int m = s.length();
    int n = t.length();

    // Initialize a table to store counts
    std::vector<std::vector<int>> dp(m + 1, std::vector<int>(n + 1, 0));

    // Base case initialization
    for (int i = 0; i <= m; ++i)
        dp[i][0] = 1; // Empty string is subsequence of all strings

    // Fill dp table in bottom-up manner
    for (int i = 1; i <= m; ++i) {
        for (int j = 1; j <= n; ++j) {
            // If last characters match, either consider or ignore
            if (s[i - 1] == t[j - 1])
                dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j];
            else
                dp[i][j] = dp[i - 1][j];
        }
    }

    // Result will be at the bottom-right corner of the dp table
    return dp[m][n];
}

int main() {
    std::string s = "abcabc";
    std::string t = "abc";

    int result = countSubsequences(s, t);
    std::cout << "Number of subsequences of '" << t << "' in '" << s << "': " << result << std::endl;

    return 0;
}
```

In this implementation:

- We create a 2D DP (Dynamic Programming) table `dp`, where `dp[i][j]` represents the number of subsequences of string `t` ending at position `j` of string `s`.
- We initialize the base case: `dp[i][0] = 1` because an empty string is a subsequence of any string.
- We iterate through both strings and update the table based on whether characters match or not.
- If the characters match, we have two choices: we can include the current character as part of the subsequence, or we can ignore it. Hence, `dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j]`.
- If the characters don't match, the number of subsequences doesn't increase, so `dp[i][j] = dp[i - 1][j]`.
- Finally, the result is stored in `dp[m][n]`, where `m` and `n` are the lengths of strings `s` and `t` respectively.

### 1. Algorithms & Data Structures (C++): Counting Subsequences Recursive

Sure, let's discuss how to count subsequences recursively in C++.

A subsequence of a string is a sequence that can be derived from the original string by deleting some or no elements without changing the order of the remaining elements. For example, "abc", "ac", "ab", etc., are subsequences of the string "abc".

Here's a recursive approach to count the number of subsequences in a string:

```cpp
#include <iostream>
#include <string>

using namespace std;

int countSubsequences(const string& str, int index, const string& target) {
    // If the target string is empty, it is a valid subsequence
    if (target.size() == 0) {
        return 1;
    }

    // If the index reaches the end of the string, there are no more subsequences
    if (index == str.size()) {
        return 0;
    }

    int count = 0;

    // If the characters match, we can either include or exclude the current character
    if (str[index] == target[0]) {
        count += countSubsequences(str, index + 1, target.substr(1)); // Include the current character
        count += countSubsequences(str, index + 1, target); // Exclude the current character
    } else {
        // If the characters don't match, we can only exclude the current character
        count += countSubsequences(str, index + 1, target);
    }

    return count;
}

int main() {
    string str = "abc";
    string target = "abc";

    cout << "Number of subsequences: " << countSubsequences(str, 0, target) << endl;

    return 0;
}
```

In this code:

- The `countSubsequences` function takes three arguments: the original string `str`, the current index `index`, and the target string `target` (which is the subsequence we are trying to form).
- At each step, we have two choices: include the current character or exclude it. If the current character matches the first character of the target string, we explore both options. If it doesn't match, we can only exclude the current character.
- The base cases are when the target string becomes empty (indicating we have found a valid subsequence) or when we reach the end of the string `str`.

This recursive approach explores all possible combinations of including or excluding characters, leading to an exponential time complexity.

### 1. Algorithms & Data Structures (C++): Counting Words and Vowels in a String

Certainly! Here's a simple implementation in C++ to count words and vowels in a string:

```cpp
#include <iostream>
#include <string>
#include <cctype> // for isalpha() and tolower()

using namespace std;

int countWords(const string& str) {
    int count = 0;
    bool inWord = false;

    for (char c : str) {
        if (isalpha(c)) {
            if (!inWord) {
                inWord = true;
                count++;
            }
        } else {
            inWord = false;
        }
    }

    return count;
}

int countVowels(const string& str) {
    int count = 0;

    for (char c : str) {
        char lowercase_c = tolower(c);
        if (lowercase_c == 'a' || lowercase_c == 'e' || lowercase_c == 'i' || lowercase_c == 'o' || lowercase_c == 'u') {
            count++;
        }
    }

    return count;
}

int main() {
    string input;
    cout << "Enter a string: ";
    getline(cin, input);

    int numWords = countWords(input);
    int numVowels = countVowels(input);

    cout << "Number of words: " << numWords << endl;
    cout << "Number of vowels: " << numVowels << endl;

    return 0;
}
```

This code defines two functions: `countWords()` and `countVowels()`, which count the number of words and vowels in a given string, respectively. In the `main()` function, it prompts the user to input a string, then it calls these functions and prints out the results.

### 1. Algorithms & Data Structures (C++): Data Structure: Character Array

In C++, a character array is a fundamental data structure used to store sequences of characters. It's essentially a contiguous block of memory where each element represents a single character. Here's a basic overview of working with character arrays in C++:

#### Declaration and Initialization

You can declare a character array like this:

```cpp
char charArray[SIZE]; // Where SIZE is the maximum number of characters in the array
```

And you can initialize it either statically or dynamically:

```cpp
char charArray[] = {'H', 'e', 'l', 'l', 'o', '\0'}; // Static initialization with a null terminator
```

#### Operations

1. **Accessing Elements:** You can access individual elements of the array using the index notation:

```cpp
charArray[0]; // Accesses the first element ('H')
```

1. **String Input:** You can use the `cin` function for taking input into a character array:

```cpp
cin >> charArray; // Reads a string input into the character array
```

1. **String Output:** You can use the `cout` function for outputting a character array:

```cpp
cout << charArray; // Outputs the string stored in the character array
```

1. **String Manipulation:** You can manipulate character arrays using standard library functions from `<cstring>` like `strcpy`, `strcat`, `strlen`, etc.

#### Example

```cpp
#include <iostream>
#include <cstring>

using namespace std;

int main() {
    char greeting[6] = {'H', 'e', 'l', 'l', 'o', '\0'};

    cout << "Greeting message: ";
    cout << greeting << endl;

    char str1[10] = "Hello";
    char str2[10] = "World";
    char str3[10];

    strcpy(str3, str1); // Copy str1 into str3
    strcat(str3, str2); // Concatenate str2 onto str3

    cout << "Concatenated string: " << str3 << endl;

    return 0;
}
```

#### Note

- Ensure that you have enough memory allocated for your character array, including space for the null terminator (`\0`) if you're working with C-style strings.
- Be cautious about buffer overflows, as C++ does not provide automatic bounds checking for arrays.
- If you're working with strings, consider using the `std::string` class from the C++ Standard Library, which provides safer and more convenient string manipulation methods.

### 1. Algorithms & Data Structures (C++): Data Structure: String

In C++, a string is a sequence of characters stored in a data structure. C++ offers two main ways to handle strings:

1. **C-Style Strings (Character Arrays)**:
   In C, strings are represented as arrays of characters terminated by a null character '\0'. You can use character arrays to work with strings in C++, but it's not as convenient as the `std::string` class. Here's a basic example of using C-style strings:

   ```cpp
   #include <iostream>
   #include <cstring> // for C string functions

   int main() {
       char str[] = "Hello"; // defining a character array
       std::cout << "String: " << str << std::endl;

       // Using C string functions
       std::cout << "Length: " << strlen(str) << std::endl; // string length
       std::cout << "First character: " << str[0] << std::endl;
       // and so on...

       return 0;
   }
   ```

2. **`std::string` Class**:
   This is the preferred way to handle strings in C++. It's part of the C++ Standard Library and provides a rich set of methods to manipulate strings. Here's how you can use it:

   ```cpp
   #include <iostream>
   #include <string> // for string class

   int main() {
       std::string str = "Hello"; // defining a string object
       std::cout << "String: " << str << std::endl;

       // Using string methods
       std::cout << "Length: " << str.length() << std::endl; // string length
       std::cout << "First character: " << str[0] << std::endl;
       // and so on...

       return 0;
   }
   ```

   With `std::string`, you don't need to worry about managing memory manually, as it dynamically allocates and deallocates memory as needed. Plus, it provides many useful methods like `length()`, `append()`, `substr()`, `find()`, and more.

In general, it's recommended to use `std::string` unless you have a specific reason to use C-style strings. It provides safer and more convenient string handling capabilities.

### 1. Algorithms & Data Structures (C++): Determining if a String is a Palindrome

Sure, determining if a string is a palindrome is a common programming problem. A palindrome is a word, phrase, number, or other sequence of characters that reads the same forward and backward, ignoring spaces, punctuation, and capitalization. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <string>
#include <algorithm>

bool isPalindrome(const std::string& str) {
    // Create a copy of the string with only alphanumeric characters
    std::string cleanStr;
    for (char c : str) {
        if (std::isalnum(c)) {
            cleanStr += std::tolower(c);
        }
    }
    
    // Reverse the cleaned string
    std::string reversedStr = cleanStr;
    std::reverse(reversedStr.begin(), reversedStr.end());
    
    // Compare the original and reversed strings
    return cleanStr == reversedStr;
}

int main() {
    std::string input;
    std::cout << "Enter a string: ";
    std::getline(std::cin, input);

    if (isPalindrome(input)) {
        std::cout << input << " is a palindrome." << std::endl;
    } else {
        std::cout << input << " is not a palindrome." << std::endl;
    }

    return 0;
}
```

This code defines a function `isPalindrome()` that takes a string as input and returns `true` if the string is a palindrome, and `false` otherwise. In the `main()` function, the user is prompted to enter a string, and then the `isPalindrome()` function is called to check if the entered string is a palindrome or not.

The function first creates a copy of the input string with only alphanumeric characters (ignoring spaces, punctuation, and capitalization). Then it reverses this cleaned string and compares it with the original cleaned string to determine if it's a palindrome or not.

### 1. Algorithms & Data Structures (C++): Exercise: Find The Vowels

Sure, here's a simple C++ program to find the vowels in a given string:

```cpp
#include <iostream>
#include <string>
#include <unordered_set>

std::unordered_set<char> vowels = {'a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'};

void findVowels(const std::string& str) {
    std::cout << "Vowels in the string: ";
    for (char ch : str) {
        if (vowels.find(ch) != vowels.end()) {
            std::cout << ch << " ";
        }
    }
    std::cout << std::endl;
}

int main() {
    std::string input;
    std::cout << "Enter a string: ";
    std::getline(std::cin, input);
    
    findVowels(input);
    
    return 0;
}
```

This program defines a set of vowels and then iterates through each character in the input string. If the character is found in the set of vowels, it's printed out. Finally, it displays all the vowels found in the string.

### 1. Algorithms & Data Structures (C++): Exercise: Max Chars Problem

Sure, the "Max Chars Problem" typically refers to a common interview question: given a string, find the character that appears the most frequently in the string.

Here's how you could solve it in C++:

```cpp
#include <iostream>
#include <string>
#include <unordered_map>

char maxChars(const std::string& str) {
    std::unordered_map<char, int> charCount;

    // Count occurrences of each character
    for (char c : str) {
        charCount[c]++;
    }

    char maxChar = '\0';
    int maxCount = 0;

    // Find the character with the maximum count
    for (const auto& pair : charCount) {
        if (pair.second > maxCount) {
            maxChar = pair.first;
            maxCount = pair.second;
        }
    }

    return maxChar;
}

int main() {
    std::string str = "Hello World";
    char maxChar = maxChars(str);
    std::cout << "The character '" << maxChar << "' appears the most in the string." << std::endl;
    return 0;
}
```

This code creates a hash map (`std::unordered_map`) to store the count of each character in the string. Then, it iterates through the string to count the occurrences of each character. Finally, it iterates through the map to find the character with the maximum count.

The time complexity of this solution is O(n), where n is the length of the string.

### 1. Algorithms & Data Structures (C++): Exercise: Sentence Capitalization

For the "Sentence Capitalization" exercise, you can write a C++ function that takes a string as input and capitalizes the first letter of each sentence. Here's a sample implementation:

```cpp
#include <iostream>
#include <string>
#include <cctype>

void capitalizeSentences(std::string &text) {
    bool capitalizeNext = true;
    
    for (char &c : text) {
        if (capitalizeNext && std::isalpha(c)) {
            c = std::toupper(c);
            capitalizeNext = false;
        } else if (c == '.' || c == '!' || c == '?') {
            capitalizeNext = true;
        }
    }
}

int main() {
    std::string text = "this is a sample text. it has multiple sentences! can you capitalize them? let's see.";
    
    std::cout << "Original text:\n" << text << std::endl;
    
    capitalizeSentences(text);
    
    std::cout << "\nCapitalized text:\n" << text << std::endl;
    
    return 0;
}
```

This program defines a function `capitalizeSentences` that takes a string reference and iterates over each character. It checks if a character is an alphabet and if it's the first character of a sentence (i.e., after '.', '!', or '?'). If so, it capitalizes it using `std::toupper`. Then, it updates the flag `capitalizeNext` accordingly.

The `main` function demonstrates the usage of this function by applying it to a sample text. You can replace the sample text with any other text you want to test.

### 1. Algorithms & Data Structures (C++): Exercise: Solving Anagrams

Sure, solving anagrams is an interesting problem! In C++, you can approach this in several ways, but one common method is to use sorting. Here's a simple algorithm to solve anagrams in C++:

```cpp
#include <iostream>
#include <string>
#include <algorithm>
#include <unordered_map>
#include <vector>

using namespace std;

// Function to check if two strings are anagrams
bool areAnagrams(const string& str1, const string& str2) {
    if (str1.length() != str2.length())
        return false;

    string s1 = str1, s2 = str2;
    sort(s1.begin(), s1.end());
    sort(s2.begin(), s2.end());

    return s1 == s2;
}

// Function to group anagrams together in a vector of strings
vector<vector<string>> groupAnagrams(const vector<string>& words) {
    unordered_map<string, vector<string>> anagramGroups;

    for (const string& word : words) {
        string sortedWord = word;
        sort(sortedWord.begin(), sortedWord.end());
        anagramGroups[sortedWord].push_back(word);
    }

    vector<vector<string>> result;
    for (auto& pair : anagramGroups) {
        result.push_back(pair.second);
    }

    return result;
}

int main() {
    vector<string> words = {"listen", "silent", "hello", "world", "cat", "tac", "heart", "earth"};

    cout << "Anagram Groups:\n";
    vector<vector<string>> anagramGroups = groupAnagrams(words);
    for (const auto& group : anagramGroups) {
        for (const string& word : group) {
            cout << word << " ";
        }
        cout << endl;
    }

    return 0;
}
```

In this code:

- `areAnagrams` function checks if two strings are anagrams by sorting them and comparing.
- `groupAnagrams` function groups anagrams together by sorting each word and using an unordered_map to store them.
- In the `main` function, we define a vector of strings and call `groupAnagrams` to group them. Then, we print out the grouped anagrams.

This is just one way to solve the problem. There are more optimized solutions available, especially if performance is a concern. For example, you can use a hashing approach to solve this problem more efficiently. Let me know if you'd like to explore that approach!

### 1. Algorithms & Data Structures (C++): Exercise: String Reversal

Sure, I'd be happy to help you with that! Reversing a string is a common problem used to demonstrate proficiency in programming languages and algorithms. Here's a simple implementation in C++:

```cpp
#include <iostream>
#include <string>

// Function to reverse a string
std::string reverseString(const std::string& str) {
    int n = str.length();
    std::string reversedString = str;
    
    for (int i = 0; i < n / 2; i++) {
        char temp = reversedString[i];
        reversedString[i] = reversedString[n - i - 1];
        reversedString[n - i - 1] = temp;
    }
    
    return reversedString;
}

int main() {
    std::string inputString;
    
    // Input the string
    std::cout << "Enter a string: ";
    std::cin >> inputString;
    
    // Reverse the string
    std::string reversed = reverseString(inputString);
    
    // Output the reversed string
    std::cout << "Reversed string: " << reversed << std::endl;
    
    return 0;
}
```

This code defines a function `reverseString` which takes a string as input and returns its reverse. In the `main` function, it reads a string from the user, passes it to `reverseString`, and then prints the reversed string.

Feel free to ask if you have any questions or need further explanation!

### 1. Algorithms & Data Structures (C++): Exercise: What Are Anagrams?

Sure, let's tackle this exercise!

Anagrams are words or phrases that have the same characters but in a different order. For example, "listen" and "silent" are anagrams of each other because they contain the same letters. To determine if two strings are anagrams, we can compare their sorted versions; if they are equal after sorting, then they are anagrams.

Here's how you can implement a function in C++ to check if two strings are anagrams:

```cpp
#include <iostream>
#include <algorithm>
#include <string>

bool areAnagrams(const std::string& str1, const std::string& str2) {
    // Check if the lengths of the strings are different
    if (str1.length() != str2.length()) {
        return false;
    }

    // Sort both strings
    std::string sortedStr1 = str1;
    std::string sortedStr2 = str2;
    std::sort(sortedStr1.begin(), sortedStr1.end());
    std::sort(sortedStr2.begin(), sortedStr2.end());

    // Compare sorted strings
    return sortedStr1 == sortedStr2;
}

int main() {
    std::string str1, str2;
    std::cout << "Enter the first string: ";
    std::cin >> str1;
    std::cout << "Enter the second string: ";
    std::cin >> str2;

    if (areAnagrams(str1, str2)) {
        std::cout << str1 << " and " << str2 << " are anagrams." << std::endl;
    } else {
        std::cout << str1 << " and " << str2 << " are not anagrams." << std::endl;
    }

    return 0;
}
```

This program prompts the user to input two strings and then checks if they are anagrams using the `areAnagrams` function. It sorts both strings and compares them. If they are equal, it prints that the strings are anagrams; otherwise, it prints that they are not anagrams.

You can compile and run this code to see how it works. Let me know if you have any questions or if you'd like to explore anything further!

### 1. Algorithms & Data Structures (C++): Finding Duplicates in a String

To find duplicates in a string using C++, you can employ various approaches. Here's one common method using a hash table:

```cpp
#include <iostream>
#include <unordered_map>

void findDuplicates(const std::string& str) {
    // Create a hash table to store character frequencies
    std::unordered_map<char, int> frequencyMap;

    // Traverse the string and populate the frequency map
    for (char ch : str) {
        // Increment the frequency of character ch
        frequencyMap[ch]++;
    }

    // Traverse the frequency map to find duplicates
    for (const auto& pair : frequencyMap) {
        if (pair.second > 1) {
            std::cout << "Duplicate character: " << pair.first << ", count: " << pair.second << std::endl;
        }
    }
}

int main() {
    std::string str = "hello world";
    std::cout << "String: " << str << std::endl;
    findDuplicates(str);
    return 0;
}
```

This code snippet defines a function `findDuplicates` that takes a string as input and uses an unordered map (`std::unordered_map`) to store the frequency of each character in the string. Then, it traverses the map to identify characters with frequencies greater than 1, indicating duplicates.

For instance, if you run this code with the string "hello world", it will output:

```bash
String: hello world
Duplicate character: l, count: 3
Duplicate character: o, count: 2
```

This approach has a time complexity of O(n), where n is the length of the string, because it iterates through the string only once. The space complexity is also O(n) due to the hash table used to store character frequencies.

### 1. Algorithms & Data Structures (C++): Finding Duplicates in a String using Bitwise Operations

Sure, you can use bitwise operations to find duplicates in a string in C++. One approach is to use a 32-bit integer as a bit vector where each bit represents the presence of a character in the string. Here's a simple implementation:

```cpp
#include <iostream>

bool hasDuplicateCharacters(const std::string& str) {
    // Assuming ASCII characters (8-bit)
    if (str.length() > 256) // No duplicates possible if string length is greater than 256
        return true;

    int checker = 0;

    for (char c : str) {
        int val = c - 'a'; // Assuming lowercase alphabets
        if ((checker & (1 << val)) > 0) {
            return true; // Duplicate found
        }
        checker |= (1 << val);
    }

    return false; // No duplicates found
}

int main() {
    std::string str = "abcdefg";
    if (hasDuplicateCharacters(str)) {
        std::cout << "String has duplicate characters." << std::endl;
    } else {
        std::cout << "String does not have duplicate characters." << std::endl;
    }
    return 0;
}
```

In this implementation:

- We assume ASCII characters, so we create a bit vector of size 256.
- We iterate through each character in the string and calculate its position in the bit vector by subtracting the ASCII value of 'a' from the character's ASCII value.
- If the corresponding bit in the bit vector is already set, it means we've encountered the character before, so we return true.
- Otherwise, we set the bit at that position in the bit vector.
- If we reach the end of the string without finding any duplicates, we return false.

This algorithm has a time complexity of O(n), where n is the length of the string, and a space complexity of O(1) since the size of the bit vector is fixed.

### 1. Algorithms & Data Structures (C++): Finding Length of a String

Certainly! In C++, you can find the length of a string using the `length()` or `size()` member functions of the `std::string` class. Here's a simple example:

```cpp
#include <iostream>
#include <string>

int main() {
    std::string str = "Hello, World!";
    
    // Using length() function
    int len1 = str.length();

    // Using size() function
    int len2 = str.size();

    std::cout << "Length of the string (using length()): " << len1 << std::endl;
    std::cout << "Length of the string (using size()): " << len2 << std::endl;

    return 0;
}
```

Output:

```bash
Length of the string (using length()): 13
Length of the string (using size()): 13
```

Both `length()` and `size()` functions return the number of characters in the string. You can use either of them interchangeably.

### 1. Algorithms & Data Structures (C++): Finding Prefixes of Strings

In C++, you can find prefixes of strings using various algorithms and data structures. One common approach is to use a trie data structure. A trie is a tree-like data structure that stores a dynamic set of strings where the keys can be represented by sequences of characters.

Here's a simple implementation of a trie in C++ that allows you to insert strings and find their prefixes:

```cpp
#include <iostream>
#include <unordered_map>
using namespace std;

class TrieNode {
public:
    unordered_map<char, TrieNode*> children;
    bool isEndOfWord;

    TrieNode() {
        isEndOfWord = false;
    }
};

class Trie {
private:
    TrieNode* root;

public:
    Trie() {
        root = new TrieNode();
    }

    void insert(const string& word) {
        TrieNode* current = root;
        for (char ch : word) {
            if (current->children.find(ch) == current->children.end()) {
                current->children[ch] = new TrieNode();
            }
            current = current->children[ch];
        }
        current->isEndOfWord = true;
    }

    void findPrefixesUtil(TrieNode* node, string prefix) {
        if (node->isEndOfWord) {
            cout << prefix << endl;
        }
        for (auto& pair : node->children) {
            findPrefixesUtil(pair.second, prefix + pair.first);
        }
    }

    void findPrefixes(const string& prefix) {
        TrieNode* current = root;
        for (char ch : prefix) {
            if (current->children.find(ch) == current->children.end()) {
                cout << "No words with the given prefix found." << endl;
                return;
            }
            current = current->children[ch];
        }
        findPrefixesUtil(current, prefix);
    }
};

int main() {
    Trie trie;
    trie.insert("apple");
    trie.insert("app");
    trie.insert("apricot");
    trie.insert("banana");
    
    cout << "Prefixes for 'ap':" << endl;
    trie.findPrefixes("ap");

    return 0;
}
```

This code defines a TrieNode class representing nodes in the trie, and a Trie class implementing the trie data structure. The insert function inserts strings into the trie, and the findPrefixes function finds all prefixes of a given string. You can customize and extend this code to suit your specific requirements.

### 1. Algorithms & Data Structures (C++): Finding Substring

Sure, finding a substring within a string is a common task in programming. There are several ways to approach this problem, but let's discuss a simple and efficient algorithm: the Knuth-Morris-Pratt (KMP) algorithm. Here's a brief overview of how it works:

1. **Preprocessing (Building the Partial Match Table)**: The first step is to build a partial match table for the substring we're searching for. This table helps us avoid unnecessary comparisons by exploiting the information about the previously matched characters.

2. **Searching**: Once the partial match table is constructed, we use it to guide the search through the main string. By shifting the substring intelligently based on the information in the partial match table, we avoid rechecking characters that we know will not lead to a match.

Here's a C++ implementation of the KMP algorithm:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

// Function to build the partial match table (LPS array)
vector<int> buildLPS(string pattern) {
    int m = pattern.length();
    vector<int> lps(m, 0); // Initialize the LPS array with zeros
    int len = 0; // Length of the previous longest prefix suffix

    // i traverses from index 1 to m-1
    int i = 1;
    while (i < m) {
        if (pattern[i] == pattern[len]) {
            len++;
            lps[i] = len;
            i++;
        }
        else {
            if (len != 0) {
                len = lps[len - 1];
            }
            else {
                lps[i] = 0;
                i++;
            }
        }
    }
    return lps;
}

// Function to perform substring search using KMP algorithm
vector<int> findSubstring(string text, string pattern) {
    vector<int> result;
    int n = text.length();
    int m = pattern.length();
    vector<int> lps = buildLPS(pattern);
    int i = 0; // Index for text[]
    int j = 0; // Index for pattern[]

    while (i < n) {
        if (pattern[j] == text[i]) {
            i++;
            j++;
        }

        if (j == m) { // If pattern is found
            result.push_back(i - j);
            j = lps[j - 1];
        }

        // Mismatch after j matches
        else if (i < n && pattern[j] != text[i]) {
            if (j != 0)
                j = lps[j - 1];
            else
                i = i + 1;
        }
    }
    return result;
}

// Example usage
int main() {
    string text = "ABABDABACDABABCABAB";
    string pattern = "ABABCABAB";
    vector<int> positions = findSubstring(text, pattern);

    if (positions.empty())
        cout << "Pattern not found in the text.\n";
    else {
        cout << "Pattern found at positions: ";
        for (int pos : positions) {
            cout << pos << " ";
        }
        cout << endl;
    }

    return 0;
}
```

This implementation efficiently finds all occurrences of a substring within a given string. The time complexity of the KMP algorithm is O(n + m), where n is the length of the text and m is the length of the pattern, making it quite efficient for large texts and patterns.

### 1. Algorithms & Data Structures (C++): Finding the Longest Palindromic Substring

Finding the longest palindromic substring is a classic problem in computer science. Here's a C++ implementation using dynamic programming:

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

string longestPalindromicSubstring(string s) {
    int n = s.length();
    if (n == 0)
        return "";

    vector<vector<bool>> dp(n, vector<bool>(n, false));

    int maxLength = 1;
    int start = 0;

    // All substrings of length 1 are palindromes
    for (int i = 0; i < n; i++)
        dp[i][i] = true;

    // Check for substrings of length 2
    for (int i = 0; i < n - 1; i++) {
        if (s[i] == s[i + 1]) {
            dp[i][i + 1] = true;
            start = i;
            maxLength = 2;
        }
    }

    // Check for substrings of length greater than 2
    for (int len = 3; len <= n; len++) {
        for (int i = 0; i < n - len + 1; i++) {
            int j = i + len - 1;
            if (s[i] == s[j] && dp[i + 1][j - 1]) {
                dp[i][j] = true;
                if (len > maxLength) {
                    start = i;
                    maxLength = len;
                }
            }
        }
    }

    return s.substr(start, maxLength);
}

int main() {
    string s = "babad";
    cout << "Longest Palindromic Substring: " << longestPalindromicSubstring(s) << endl;
    return 0;
}
```

This implementation uses dynamic programming to solve the problem in O(n^2) time complexity and O(n^2) space complexity, where n is the length of the input string. It fills a 2D DP table where `dp[i][j]` represents whether the substring from index `i` to `j` is a palindrome or not. Then, it iterates over all possible substrings to find the longest palindromic substring.

### 1. Algorithms & Data Structures (C++): Finding the Longest Palindromic Substring: analysis

Finding the longest palindromic substring is a classic problem in computer science and can be solved efficiently using dynamic programming or various other approaches. Let's break down one of the dynamic programming solutions and analyze its time and space complexity.

#### Dynamic Programming Approach

1. **Initialization:**
   - Initialize a 2D boolean array `dp` of size NxN, where N is the length of the input string.
   - `dp[i][j]` will be true if the substring from index `i` to `j` is a palindrome.

2. **Base Cases:**
   - Single characters are always palindromes, so `dp[i][i]` is set to true for all `i`.
   - For substrings of length 2, `dp[i][i+1]` is true if the characters at indices `i` and `i+1` are the same.

3. **Dynamic Programming Step:**
   - For substrings of length greater than 2, `dp[i][j]` is true if the characters at indices `i` and `j` are equal and `dp[i+1][j-1]` is also true.

4. **Tracking the Longest Palindromic Substring:**
   - While updating `dp`, keep track of the longest palindromic substring encountered.

#### Time Complexity Analysis

- Constructing the `dp` table takes O(N^2) time, where N is the length of the input string.
- For each cell of the `dp` table, we need to check if the substring is a palindrome, which takes constant time.
- So, the overall time complexity is O(N^2).

#### Space Complexity Analysis

- We use a 2D boolean array of size NxN for dynamic programming, resulting in O(N^2) space complexity.
- Additionally, we need O(1) space for storing indices of the longest palindromic substring.
- Hence, the overall space complexity is O(N^2).

#### Example

Let's say the input string is "babad".

- Constructing the `dp` table:

  ```bash
      b  a  b  a  d
   b  T  F  T  F  F
   a     T  F  T  F
   b        T  F  F
   a           T  F
   d              T
  ```

- The longest palindromic substring is "bab" or "aba".

Dynamic programming offers an efficient solution to this problem, providing a clear understanding of the substrings that are palindromes and enabling us to track the longest palindromic substring efficiently.

### 1. Algorithms & Data Structures (C++): Finding the Longest Palindromic Substring: improved

Improving the algorithm for finding the longest palindromic substring can involve dynamic programming or an optimized approach using Manacher's algorithm. Here's an optimized approach using Manacher's algorithm, which has a linear runtime complexity:

```cpp
#include <iostream>
#include <string>
#include <vector>

std::string longestPalindrome(const std::string& s) {
    if (s.empty()) return "";

    // Preprocess the string to insert special characters
    std::string processed = "#";
    for (char c : s) {
        processed += c;
        processed += '#';
    }

    int n = processed.size();
    std::vector<int> p(n, 0); // p[i] stores the length of the palindrome centered at i
    int center = 0, right = 0;

    for (int i = 1; i < n - 1; ++i) {
        int mirror = 2 * center - i; // mirror of i with respect to center
        if (i < right)
            p[i] = std::min(right - i, p[mirror]);

        // Attempt to expand palindrome centered at i
        while (processed[i + (1 + p[i])] == processed[i - (1 + p[i])])
            ++p[i];

        // If palindrome centered at i expands past right,
        // adjust center and right boundary
        if (i + p[i] > right) {
            center = i;
            right = i + p[i];
        }
    }

    // Find the longest palindrome
    int maxLen = 0, centerIndex = 0;
    for (int i = 1; i < n - 1; ++i) {
        if (p[i] > maxLen) {
            maxLen = p[i];
            centerIndex = i;
        }
    }

    int start = (centerIndex - maxLen) / 2;
    return s.substr(start, maxLen);
}

int main() {
    std::string s = "babad";
    std::cout << longestPalindrome(s) << std::endl; // Output: "bab" or "aba"
    return 0;
}
```

This algorithm iterates through the processed string only once, making it efficient. It maintains the center and right boundary of the current longest palindrome and utilizes symmetry to avoid unnecessary comparisons. Finally, it returns the longest palindrome found.

### 1. Algorithms & Data Structures (C++): Finding the Longest Palindromic Substring: Manacher's Algorithm: analysis

Manacher's Algorithm is an efficient way to find the longest palindromic substring in linear time complexity O(n), where n is the length of the input string. It's an extension of the idea behind the naive approach of checking each possible substring for palindromicity.

Here's a breakdown of how Manacher's Algorithm works:

1. **Understanding Palindromes:**
   - A palindrome is a string that reads the same forwards and backwards.
   - In a palindromic string, the characters mirror around the center. For example, "aba" and "abba" are palindromic.

2. **Preprocessing the Input String:**
   - To handle both even and odd length palindromes uniformly, we can insert special characters (usually '#') between every character and at the beginning and end of the string.
   - For example, "aba" becomes "#a#b#a#", and "abba" becomes "#a#b#b#a#".

3. **Understanding the "Palindrome Radius" Array:**
   - Manacher's Algorithm maintains an auxiliary array called the "palindrome radius array" (often denoted as P) of the same length as the modified string.
   - Each element P[i] represents the radius of the longest palindromic substring centered at index i in the modified string.
   - For the special characters inserted, P[i] represents the length of the palindrome centered at the original character in the input string.

4. **Finding Palindromic Substrings:**
   - The key insight of Manacher's Algorithm is exploiting the symmetry of palindromes to avoid unnecessary re-computation.
   - At each position i in the modified string, Manacher's Algorithm efficiently computes P[i] by utilizing previously computed values.
   - It maintains two variables, center and right, representing the center and rightmost boundary of the "current palindrome," respectively.
   - By cleverly updating the values of center and right as it scans through the string, the algorithm can determine the palindrome radius at each position without rechecking characters unnecessarily.

5. **Finding the Longest Palindromic Substring:**
   - Once the palindrome radius array is constructed, the longest palindromic substring can be found by identifying the maximum value in the array and extracting the corresponding substring.

6. **Complexity Analysis:**
   - The time complexity of Manacher's Algorithm is O(n), where n is the length of the input string. This is because the algorithm scans the input string only once, and at each position, it performs constant-time operations.
   - The space complexity is also O(n) due to the auxiliary palindrome radius array.

In summary, Manacher's Algorithm is an elegant and efficient approach to finding the longest palindromic substring, leveraging symmetry and avoiding redundant computations to achieve linear time complexity.

### 1. Algorithms & Data Structures (C++): Finding the Longest Palindromic Substring: Manacher's Algorithm: impl

Implementing Manacher's Algorithm in C++ to find the longest palindromic substring involves a few steps. Here's a basic implementation:

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

string longestPalindromicSubstring(string s) {
    string T = "#"; // Inserting # between characters to handle even-length palindromes
    for (char c : s) {
        T += c;
        T += '#';
    }
    
    int n = T.size();
    vector<int> P(n, 0); // Array to store lengths of palindromes centered at each position
    int center = 0; // Center of the currently known longest palindromic substring
    int maxRight = 0; // Right boundary of the currently known longest palindromic substring
    
    for (int i = 1; i < n - 1; i++) {
        int mirror = 2 * center - i; // mirror of i with respect to center
        if (i < maxRight) {
            P[i] = min(maxRight - i, P[mirror]);
        }
        
        // Attempt to expand palindrome centered at i
        while (T[i + 1 + P[i]] == T[i - 1 - P[i]]) {
            P[i]++;
        }
        
        // If palindrome centered at i expands past maxRight,
        // adjust center and maxRight accordingly
        if (i + P[i] > maxRight) {
            center = i;
            maxRight = i + P[i];
        }
    }
    
    // Find the maximum element in P
    int maxLen = 0, maxCenter = 0;
    for (int i = 1; i < n - 1; i++) {
        if (P[i] > maxLen) {
            maxLen = P[i];
            maxCenter = i;
        }
    }
    
    // Extract the longest palindromic substring from T
    int start = (maxCenter - maxLen) / 2;
    return s.substr(start, maxLen);
}

int main() {
    string s = "babad";
    cout << "Longest palindromic substring: " << longestPalindromicSubstring(s) << endl;
    return 0;
}
```

This implementation defines a function `longestPalindromicSubstring` that takes a string `s` as input and returns the longest palindromic substring. The `main` function demonstrates its usage with a sample string. Manacher's algorithm efficiently finds the longest palindromic substring in linear time complexity.

### 1. Algorithms & Data Structures (C++): First Non-Repeating

To find the first non-repeating character in a string using C++, you can use a hash map to store the frequency of each character and then iterate through the string to find the first character with a frequency of 1. Here's how you can implement this algorithm:

```cpp
#include <iostream>
#include <unordered_map>
#include <string>

char firstNonRepeatingChar(const std::string& str) {
    std::unordered_map<char, int> charCount;

    // Count the frequency of each character
    for (char c : str) {
        charCount[c]++;
    }

    // Find the first non-repeating character
    for (char c : str) {
        if (charCount[c] == 1) {
            return c;
        }
    }

    // If no non-repeating character found, return a null character
    return '\0';
}

int main() {
    std::string str = "hello";
    char firstNonRepeating = firstNonRepeatingChar(str);
    if (firstNonRepeating != '\0') {
        std::cout << "First non-repeating character: " << firstNonRepeating << std::endl;
    } else {
        std::cout << "No non-repeating character found." << std::endl;
    }
    return 0;
}
```

In this code:

- We first create an unordered map `charCount` to store the frequency of each character in the string.
- We iterate through the string and update the frequency count for each character.
- Then, we iterate through the string again and return the first character with a frequency of 1.
- If no non-repeating character is found, we return a null character.

You can modify the `main` function to test this algorithm with different strings.

### 1. Algorithms & Data Structures (C++): First Non-Repeating Character

To find the first non-repeating character in a string using C++, you can employ a hashmap to count the occurrences of each character and then iterate through the string to find the first character with a count of 1. Here's a sample implementation:

```cpp
#include <iostream>
#include <unordered_map>
#include <string>

char firstNonRepeatingChar(const std::string& str) {
    std::unordered_map<char, int> charCount;

    // Count occurrences of each character
    for (char ch : str) {
        charCount[ch]++;
    }

    // Find the first non-repeating character
    for (char ch : str) {
        if (charCount[ch] == 1) {
            return ch;
        }
    }

    // If no non-repeating character found, return '\0'
    return '\0';
}

int main() {
    std::string str = "leetcode";
    char firstNonRepeating = firstNonRepeatingChar(str);
    
    if (firstNonRepeating != '\0') {
        std::cout << "The first non-repeating character in \"" << str << "\" is: " << firstNonRepeating << std::endl;
    } else {
        std::cout << "There is no non-repeating character in \"" << str << "\"" << std::endl;
    }
    
    return 0;
}
```

This code first counts the occurrences of each character in the string using an unordered map (`std::unordered_map`). Then, it iterates through the string again to find the first character with a count of 1, indicating that it is not repeated. If no such character is found, it returns `'\0'`.

### 1. Algorithms & Data Structures (C++): First Non-Repeating Letter

To find the first non-repeating letter in a string using C++, you can employ an algorithm that counts the occurrences of each character and then iterates through the string to find the first character with a count of 1. Here's a C++ implementation:

```cpp
#include <iostream>
#include <unordered_map>

char firstNonRepeatingLetter(const std::string& str) {
    std::unordered_map<char, int> charCount;

    // Count occurrences of each character
    for (char c : str) {
        charCount[c]++;
    }

    // Find the first non-repeating character
    for (char c : str) {
        if (charCount[c] == 1) {
            return c;
        }
    }

    // If no non-repeating character found, return '\0' (null character)
    return '\0';
}

int main() {
    std::string str = "aabbccddeeffg";
    char result = firstNonRepeatingLetter(str);
    if (result != '\0') {
        std::cout << "The first non-repeating letter is: " << result << std::endl;
    } else {
        std::cout << "No non-repeating letter found in the string." << std::endl;
    }
    return 0;
}
```

This code first counts the occurrences of each character in the input string using an unordered map. Then, it iterates through the string again to find the first character with a count of 1. Finally, it returns the first non-repeating character found, or '\0' if no such character is found.

### 1. Algorithms & Data Structures (C++): First repeating character

Sure, finding the first repeating character in a string is a common problem in computer science. Here's a simple algorithm to solve it in C++:

```cpp
#include <iostream>
#include <unordered_set>

char firstRepeatingChar(const std::string& str) {
    std::unordered_set<char> seenChars;
    for (char c : str) {
        if (seenChars.find(c) != seenChars.end()) {
            return c; // Found the first repeating character
        } else {
            seenChars.insert(c);
        }
    }
    return '\0'; // No repeating character found
}

int main() {
    std::string str = "abcdefgab";
    char firstRepeat = firstRepeatingChar(str);
    if (firstRepeat != '\0') {
        std::cout << "The first repeating character is: " << firstRepeat << std::endl;
    } else {
        std::cout << "No repeating character found." << std::endl;
    }
    return 0;
}
```

This code defines a function `firstRepeatingChar` that takes a string as input and returns the first repeating character in the string. It uses an `unordered_set` to keep track of characters seen so far. If a character is already in the set, it means it's repeating, and the function returns it. If no repeating character is found, it returns the null character `'\0'`. The `main` function demonstrates the usage of this function.

### 1. Algorithms & Data Structures (C++): First repeating character: Complexity analysis

Sure! Let's discuss the complexity analysis of finding the first repeating character in a given string using algorithms and data structures in C++.

Here's a common approach using a hash table (unordered_map in C++) to keep track of characters we've encountered so far:

```cpp
#include <iostream>
#include <unordered_map>

char firstRepeatingCharacter(const std::string& str) {
    std::unordered_map<char, int> charCount;
    
    for (char c : str) {
        charCount[c]++;
        if (charCount[c] > 1) {
            return c;
        }
    }
    
    return '\0'; // No repeating character found
}

int main() {
    std::string str = "abcaadef";
    char result = firstRepeatingCharacter(str);
    
    if (result != '\0') {
        std::cout << "First repeating character: " << result << std::endl;
    } else {
        std::cout << "No repeating character found." << std::endl;
    }
    
    return 0;
}
```

Let's analyze the complexity of this approach:

1. **Time Complexity**:
   - The loop iterates through each character in the input string once. So, the time complexity of the loop is O(n), where n is the length of the string.
   - Insertions and lookups in an unordered_map (hash table) typically take O(1) time on average, assuming a good hash function and a sufficiently large hash table.
   - Therefore, inside the loop, each insertion and lookup operation takes constant time.
   - Overall, the time complexity of the algorithm is O(n), where n is the length of the input string.

2. **Space Complexity**:
   - We use an unordered_map to store characters and their counts. In the worst-case scenario, we may need to store all characters of the input string along with their counts.
   - So, the space complexity is O(n), where n is the length of the input string.

This algorithm offers a linear time complexity solution, which is efficient for finding the first repeating character in a given string.

### 1. Algorithms & Data Structures (C++): First Repeating Letter

To find the first repeating letter in a given string using C++, you can employ a hash map to store the frequency of each character encountered. Here's a C++ function to achieve this:

```cpp
#include <iostream>
#include <unordered_map>

char firstRepeatingLetter(const std::string& str) {
    std::unordered_map<char, int> frequency;
    
    for (char ch : str) {
        // Increment the frequency of the current character
        frequency[ch]++;
        
        // If the frequency becomes 2, it means the character is repeating
        if (frequency[ch] == 2) {
            return ch; // Return the first repeating character
        }
    }
    
    // If no character repeats, return null character
    return '\0';
}

int main() {
    std::string input;
    std::cout << "Enter a string: ";
    std::cin >> input;
    
    char result = firstRepeatingLetter(input);
    if (result != '\0') {
        std::cout << "The first repeating letter is: " << result << std::endl;
    } else {
        std::cout << "No repeating letter found." << std::endl;
    }
    
    return 0;
}
```

This code defines a function `firstRepeatingLetter` which takes a string as input and returns the first repeating letter in the string. Inside this function, a hash map (`std::unordered_map`) is used to store the frequency of each character encountered. The input string is iterated character by character, and for each character, its frequency is incremented in the hash map. When the frequency of a character becomes 2, it means that character is repeating, so it returns that character. If no repeating character is found, it returns the null character `'\0'`.

In the `main` function, the user is prompted to input a string, and then the `firstRepeatingLetter` function is called on that input string. The result is then displayed.

### 1. Algorithms & Data Structures (C++): First Unique Character in a String

Certainly! In C++, you can find the first unique character in a string using various approaches. One common and efficient way is to use a hashmap (unordered_map in C++) to count the frequency of each character, and then iterate through the string to find the first character with a frequency of 1.

Here's how you can implement it:

```cpp
#include <iostream>
#include <unordered_map>
#include <string>

char firstUniqueChar(const std::string& s) {
    std::unordered_map<char, int> freqMap;

    // Count frequencies of each character
    for (char ch : s) {
        freqMap[ch]++;
    }

    // Find the first unique character
    for (char ch : s) {
        if (freqMap[ch] == 1) {
            return ch;
        }
    }

    // If no unique character found, return a sentinel value
    return '\0'; // Or any other suitable indication
}

int main() {
    std::string input = "leetcode";
    char firstUnique = firstUniqueChar(input);
    
    if (firstUnique != '\0') {
        std::cout << "The first unique character in \"" << input << "\" is: " << firstUnique << std::endl;
    } else {
        std::cout << "No unique character found in \"" << input << "\"" << std::endl;
    }

    return 0;
}
```

In this code:

- We first create an unordered_map called `freqMap` to store the frequency of each character in the string.
- We iterate through the string once to populate the `freqMap`.
- Then, we iterate through the string again to find the first character with a frequency of 1 in `freqMap`.
- If such a character is found, we return it; otherwise, we return a sentinel value to indicate that no unique character was found.

You can adjust the main function to test different strings and handle the cases where no unique character is found as per your requirements.

### 1. Algorithms & Data Structures (C++): Get substring index

Sure, here's a simple C++ function to get the index of a substring within a given string using the brute-force method:

```cpp
#include <iostream>
#include <string>

int findSubstringIndex(const std::string& text, const std::string& pattern) {
    int n = text.length();
    int m = pattern.length();

    for (int i = 0; i <= n - m; ++i) {
        int j;
        for (j = 0; j < m; ++j) {
            if (text[i + j] != pattern[j])
                break;
        }
        if (j == m)
            return i;  // pattern found at index i
    }

    return -1;  // pattern not found
}

int main() {
    std::string text = "hello world";
    std::string pattern = "world";

    int index = findSubstringIndex(text, pattern);
    if (index != -1)
        std::cout << "Pattern found at index " << index << std::endl;
    else
        std::cout << "Pattern not found" << std::endl;

    return 0;
}
```

This function iterates through the text string and checks if the substring starting at each index matches the pattern. If a match is found, it returns the index where the pattern starts. If no match is found, it returns -1.

This is a basic implementation and may not be the most efficient for large texts or patterns. There are more advanced algorithms like Knuth-Morris-Pratt (KMP) or Boyer-Moore which provide better performance for larger inputs.

### 1. Algorithms & Data Structures (C++): Get substring index: Complexity analysis

Analyzing the complexity of an algorithm to get the index of a substring within a larger string involves understanding the techniques and data structures used. Let's break it down:

#### Naive Approach

One naive approach would be to search the entire string for the substring character by character. Here's the complexity analysis:

- **Time Complexity**:
  - In the worst case, you might have to start matching from each character in the string, then shift to the next character if there's no match.
  - Let \( n \) be the length of the string and \( m \) be the length of the substring.
  - For each character in the string, you may need to compare at most \( m \) characters in the substring.
  - So, the time complexity of this naive approach is \( O(n \times m) \).

- **Space Complexity**:
  - Constant space complexity as it doesn't use any extra space proportional to the input size. So, \( O(1) \).

#### Optimized Approaches

Several optimized algorithms, such as the Knuth-Morris-Pratt (KMP) algorithm, Rabin-Karp algorithm, or Boyer-Moore algorithm, can improve upon the naive approach.

- **Knuth-Morris-Pratt (KMP) Algorithm**:
  - **Time Complexity**: \( O(n + m) \)
  - **Space Complexity**: \( O(m) \)

- **Rabin-Karp Algorithm**:
  - **Time Complexity**: Average case \( O(n + m) \), worst-case \( O(n \times m) \) (due to hash collisions)
  - **Space Complexity**: \( O(1) \)

- **Boyer-Moore Algorithm**:
  - **Time Complexity**: Average case \( O(n + m) \), worst-case \( O(n \times m) \) (rare)
  - **Space Complexity**: \( O(m) \)

These algorithms improve upon the naive approach by exploiting different strategies like pattern preprocessing, character skipping, or hashing. They result in better average-case performance and, in some cases, even better worst-case performance.

When choosing between these algorithms, consider factors like the nature of your data, expected pattern lengths, and whether preprocessing the pattern is acceptable or not.

#### 1. Algorithms & Data Structures (C++): Get( ) Set( ) Avg( ) Max( ) functions on Array

Certainly! Below, I'll outline how you can implement the `Get()`, `Set()`, `Avg()`, and `Max()` functions on an array in C++.

Let's start with a basic implementation:

```cpp
#include <iostream>
#include <vector>
#include <stdexcept> // for std::out_of_range

class Array {
private:
    std::vector<int> data;
public:
    // Constructor
    Array(int size) : data(size) {}
    
    // Get value at index
    int Get(int index) const {
        if (index < 0 || index >= data.size()) {
            throw std::out_of_range("Index out of range");
        }
        return data[index];
    }
    
    // Set value at index
    void Set(int index, int value) {
        if (index < 0 || index >= data.size()) {
            throw std::out_of_range("Index out of range");
        }
        data[index] = value;
    }
    
    // Calculate average of array elements
    double Avg() const {
        if (data.empty()) {
            throw std::logic_error("Array is empty");
        }
        double sum = 0;
        for (int element : data) {
            sum += element;
        }
        return sum / data.size();
    }
    
    // Get maximum element in array
    int Max() const {
        if (data.empty()) {
            throw std::logic_error("Array is empty");
        }
        int max = data[0];
        for (int element : data) {
            if (element > max) {
                max = element;
            }
        }
        return max;
    }
};

int main() {
    Array arr(5);
    
    // Set values
    arr.Set(0, 10);
    arr.Set(1, 20);
    arr.Set(2, 30);
    arr.Set(3, 40);
    arr.Set(4, 50);
    
    // Get values
    std::cout << "Value at index 2: " << arr.Get(2) << std::endl;
    
    // Calculate average
    std::cout << "Average: " << arr.Avg() << std::endl;
    
    // Get maximum
    std::cout << "Maximum: " << arr.Max() << std::endl;
    
    return 0;
}
```

This implementation creates an `Array` class with methods for `Get()`, `Set()`, `Avg()`, and `Max()`. You can initialize the array with a given size and then manipulate it using these methods.

This is a simple illustration. Depending on your specific requirements, you may want to add more features or optimizations to this implementation.

### 1. Algorithms & Data Structures (C++): Group Anagrams

Grouping anagrams is a classic problem in computer science where you're given a list of strings and you need to group together strings that are anagrams of each other. Anagrams are words or phrases formed by rearranging the letters of another word or phrase, using all the original letters exactly once.

Here's a C++ implementation using a hash map to group anagrams:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
#include <algorithm>

using namespace std;

// Function to group anagrams
vector<vector<string>> groupAnagrams(vector<string>& strs) {
    unordered_map<string, vector<string>> anagramGroups;

    // Iterate through each string in the input vector
    for (const string& str : strs) {
        // Sort the characters of the string to identify anagrams
        string sortedStr = str;
        sort(sortedStr.begin(), sortedStr.end());

        // Add the string to the corresponding group in the hash map
        anagramGroups[sortedStr].push_back(str);
    }

    // Convert hash map values to vector of vectors
    vector<vector<string>> result;
    for (auto& pair : anagramGroups) {
        result.push_back(pair.second);
    }

    return result;
}

int main() {
    // Example input
    vector<string> input = {"eat", "tea", "tan", "ate", "nat", "bat"};

    // Group the anagrams
    vector<vector<string>> groupedAnagrams = groupAnagrams(input);

    // Output the grouped anagrams
    for (const auto& group : groupedAnagrams) {
        for (const string& str : group) {
            cout << str << " ";
        }
        cout << endl;
    }

    return 0;
}
```

This implementation uses a hash map (`unordered_map`) where the keys are sorted strings (anagrams will have the same sorted string) and the values are vectors of strings representing the groups of anagrams. We iterate through the input strings, sort each one, and use the sorted string as the key in the hash map to group anagrams together. Finally, we convert the hash map into a vector of vectors to output the result.

### 1. Algorithms & Data Structures (C++): Group Anagrams - Hash Table

Sure! Grouping anagrams using a hash table is an efficient approach. Anagrams are words that have the same characters but in a different order.

Here's how you can implement this in C++ using a hash table:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
#include <algorithm>

using namespace std;

vector<vector<string>> groupAnagrams(vector<string>& strs) {
    unordered_map<string, vector<string>> anagramGroups;

    // Iterate through each word
    for (const string& word : strs) {
        // Sort the characters of the word
        string sortedWord = word;
        sort(sortedWord.begin(), sortedWord.end());

        // Add the sorted word to the corresponding group in the hash table
        anagramGroups[sortedWord].push_back(word);
    }

    vector<vector<string>> result;
    // Push each group of anagrams into the result vector
    for (auto& pair : anagramGroups) {
        result.push_back(pair.second);
    }

    return result;
}

int main() {
    vector<string> words = {"eat", "tea", "tan", "ate", "nat", "bat"};
    vector<vector<string>> anagramGroups = groupAnagrams(words);

    // Print the groups of anagrams
    for (const auto& group : anagramGroups) {
        for (const string& word : group) {
            cout << word << " ";
        }
        cout << endl;
    }

    return 0;
}
```

In this code:

1. We define a function `groupAnagrams` that takes a vector of strings `strs` as input and returns a vector of vectors of strings representing groups of anagrams.
2. We create an `unordered_map` called `anagramGroups`, where the key is the sorted version of each word (the characters sorted in alphabetical order), and the value is a vector of strings containing the anagrams of that sorted word.
3. We iterate through each word in the input vector.
4. For each word, we sort its characters and use the sorted version as a key to the hash table. We then push the original word into the corresponding vector in the hash table.
5. Finally, we iterate through the hash table and push each group of anagrams into the `result` vector.

This implementation has a time complexity of O(n * k * log(k)), where n is the number of words and k is the average length of the words. This complexity arises from sorting each word before hashing.

### 1. Algorithms & Data Structures (C++): Group Anagrams - Sorting

Certainly! Grouping anagrams is a common problem in programming interviews and real-world applications. Anagrams are words or phrases formed by rearranging the letters of another word or phrase, such as "listen" and "silent." One common approach to solving this problem is by sorting each word and then grouping words with the same sorted form together.

Here's a C++ implementation of this approach:

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <unordered_map>
#include <algorithm>

using namespace std;

vector<vector<string>> groupAnagrams(const vector<string>& strs) {
    unordered_map<string, vector<string>> anagramGroups;
    
    // Iterate through each word in the input vector
    for (const string& str : strs) {
        // Sort the characters of the word
        string sortedStr = str;
        sort(sortedStr.begin(), sortedStr.end());
        
        // Add the sorted word to the corresponding group in the map
        anagramGroups[sortedStr].push_back(str);
    }
    
    // Convert the map to the desired output format
    vector<vector<string>> result;
    for (auto it = anagramGroups.begin(); it != anagramGroups.end(); ++it) {
        result.push_back(it->second);
    }
    
    return result;
}

int main() {
    vector<string> words = {"eat", "tea", "tan", "ate", "nat", "bat"};
    
    vector<vector<string>> groupedAnagrams = groupAnagrams(words);
    
    // Print the grouped anagrams
    for (const auto& group : groupedAnagrams) {
        for (const string& word : group) {
            cout << word << " ";
        }
        cout << endl;
    }
    
    return 0;
}
```

In this code:

- We define a function `groupAnagrams` that takes a vector of strings `strs` as input and returns a vector of vectors of strings representing grouped anagrams.
- We use an unordered map `anagramGroups` to store groups of anagrams. The key is the sorted form of each word, and the value is a vector of strings containing words with the same sorted form.
- We iterate through each word in the input vector. For each word, we sort its characters and add it to the corresponding group in the map.
- Finally, we convert the map to the desired output format and return the result.

The `main` function demonstrates how to use the `groupAnagrams` function with a sample input vector of strings and prints the grouped anagrams.

### 1. Algorithms & Data Structures (C++): Interleaving string (problem)

The problem of interleaving strings is a classic dynamic programming problem. Here's a brief explanation and a possible solution in C++:

### Problem Statement

Given three strings `s1`, `s2`, and `s3`, determine whether `s3` can be formed by interleaving the characters of `s1` and `s2` while preserving the order of characters from individual strings.

### Example

```
s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac" => true
s1 = "aabcc", s2 = "dbbca", s3 = "aadbbbaccc" => false
```

### Approach

This problem can be solved using dynamic programming. We define a 2D boolean array `dp` where `dp[i][j]` represents whether the first `i` characters of `s1` and the first `j` characters of `s2` can interleave to form the first `i+j` characters of `s3`. We then populate this array based on the characters of `s1`, `s2`, and `s3`.

### C++ Solution

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

bool isInterleave(string s1, string s2, string s3) {
    int m = s1.length();
    int n = s2.length();
    
    if (m + n != s3.length())
        return false;
    
    vector<vector<bool>> dp(m + 1, vector<bool>(n + 1, false));
    
    for (int i = 0; i <= m; ++i) {
        for (int j = 0; j <= n; ++j) {
            if (i == 0 && j == 0)
                dp[i][j] = true;
            else if (i == 0)
                dp[i][j] = dp[i][j - 1] && s2[j - 1] == s3[i + j - 1];
            else if (j == 0)
                dp[i][j] = dp[i - 1][j] && s1[i - 1] == s3[i + j - 1];
            else
                dp[i][j] = (dp[i - 1][j] && s1[i - 1] == s3[i + j - 1]) ||
                           (dp[i][j - 1] && s2[j - 1] == s3[i + j - 1]);
        }
    }
    
    return dp[m][n];
}

int main() {
    string s1 = "aabcc";
    string s2 = "dbbca";
    string s3 = "aadbbcbcac";

    if (isInterleave(s1, s2, s3))
        cout << "True\n";
    else
        cout << "False\n";

    return 0;
}
```

This solution has a time complexity of O(m*n), where m and n are the lengths of strings `s1` and `s2`, respectively.

### 1. Algorithms & Data Structures (C++): Interleaving string (solution)

Interleaving strings is a classic problem in computer science. Given three strings A, B, and C, we want to determine if C can be formed by interleaving characters from A and B while preserving the order of characters from both A and B.

Here's a C++ solution using dynamic programming:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

bool isInterleave(string A, string B, string C) {
    int m = A.length(), n = B.length();
    
    // If the sum of lengths of A and B is not equal to the length of C, then C cannot be an interleaving
    if(m + n != C.length()) return false;

    // dp[i][j] will be true if C[0..i+j-1] is an interleaving of A[0..i-1] and B[0..j-1].
    vector<vector<bool>> dp(m + 1, vector<bool>(n + 1, false));

    // Base cases:
    // If both A and B are empty, then C must also be empty, hence true.
    dp[0][0] = true;

    // If A is empty, then C must be same as B
    for (int j = 1; j <= n; j++) {
        dp[0][j] = (B[j - 1] == C[j - 1]) && dp[0][j - 1];
    }

    // If B is empty, then C must be same as A
    for (int i = 1; i <= m; i++) {
        dp[i][0] = (A[i - 1] == C[i - 1]) && dp[i - 1][0];
    }

    // Fill the dp table
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            dp[i][j] = (A[i - 1] == C[i + j - 1] && dp[i - 1][j]) || 
                       (B[j - 1] == C[i + j - 1] && dp[i][j - 1]);
        }
    }

    return dp[m][n];
}

int main() {
    string A = "aab";
    string B = "axy";
    string C = "aaxaby";

    if (isInterleave(A, B, C)) {
        cout << "Yes, " << C << " is an interleaving of " << A << " and " << B << endl;
    } else {
        cout << "No, " << C << " is not an interleaving of " << A << " and " << B << endl;
    }

    return 0;
}
```

This code defines a function `isInterleave` that takes three strings A, B, and C as input and returns true if C can be formed by interleaving characters from A and B, and false otherwise. The main logic is based on dynamic programming where a 2D table `dp` is used to store intermediate results.

### 1. Algorithms & Data Structures (C++): Length of Last Word

To find the length of the last word in a given string in C++, you can follow these steps:

1. Start from the end of the string and skip any trailing spaces.
2. Once you encounter a non-space character, start counting characters until you reach a space or the beginning of the string.

Here's the C++ code to implement this algorithm:

```cpp
#include <string>

int lengthOfLastWord(const std::string& s) {
    int length = 0;
    int i = s.length() - 1;

    // Skip trailing spaces
    while (i >= 0 && s[i] == ' ')
        i--;

    // Count characters until a space or the beginning of the string
    while (i >= 0 && s[i] != ' ') {
        length++;
        i--;
    }

    return length;
}

// Example usage:
#include <iostream>
int main() {
    std::string str = "Hello World";
    std::cout << "Length of last word: " << lengthOfLastWord(str) << std::endl;
    return 0;
}
```

This code will output `5` for the string "Hello World" because the last word "World" has a length of 5.

### 1. Algorithms & Data Structures (C++): Length of String

Certainly! Here's a simple C++ function to find the length of a string using the Standard Template Library (STL) in C++:

```cpp
#include <iostream>
#include <string>

int stringLength(const std::string& str) {
    return str.length(); // or simply return str.size();
}

int main() {
    std::string myString = "Hello, world!";
    std::cout << "Length of string: " << stringLength(myString) << std::endl;
    return 0;
}
```

In this code:

- The `stringLength` function takes a constant reference to a `std::string` as its parameter and returns an integer representing the length of the string.
- Within the `stringLength` function, `str.length()` or `str.size()` is used to get the length of the string.
- In the `main` function, we define a string `myString` and then call `stringLength` function passing `myString` as an argument. The length of the string is then printed.

This is a simple example of how you can find the length of a string in C++ using the standard library.

### 1. Algorithms & Data Structures (C++): Length of String using Recursion

Sure! Here's a simple C++ implementation to find the length of a string using recursion:

```cpp
#include <iostream>
using namespace std;

// Function to find the length of a string using recursion
int findLength(const char* str) {
    // Base case: if the current character is '\0', return 0
    if (*str == '\0')
        return 0;
    // Recursive case: increment count and move to the next character
    else
        return 1 + findLength(str + 1);
}

int main() {
    const char* str = "Hello, World!";
    int length = findLength(str);
    cout << "Length of the string is: " << length << endl;
    return 0;
}
```

In this code:

- The `findLength` function takes a `const char*` as input.
- If the current character is the null terminator (`'\0'`), it returns 0, indicating the end of the string.
- Otherwise, it returns 1 plus the result of calling `findLength` with the pointer incremented by 1, thus moving to the next character in the string.
- In the `main` function, we initialize a `const char*` with the string "Hello, World!" and call `findLength` with it, storing the result in `length` and printing it out.

### 1. Algorithms & Data Structures (C++): Longest Palindrome

To find the longest palindrome in a given string using C++, you can follow a dynamic programming approach. Here's a sample code:

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

string longestPalindrome(string s) {
    int n = s.length();
    if (n == 0) return "";

    vector<vector<bool>> dp(n, vector<bool>(n, false));
    int start = 0, maxLen = 1;

    // All substrings of length 1 are palindromes
    for (int i = 0; i < n; ++i)
        dp[i][i] = true;

    // Check for substrings of length 2
    for (int i = 0; i < n - 1; ++i) {
        if (s[i] == s[i + 1]) {
            dp[i][i + 1] = true;
            start = i;
            maxLen = 2;
        }
    }

    // Check for substrings of length greater than 2
    for (int len = 3; len <= n; ++len) {
        for (int i = 0; i < n - len + 1; ++i) {
            int j = i + len - 1;
            if (s[i] == s[j] && dp[i + 1][j - 1]) {
                dp[i][j] = true;
                start = i;
                maxLen = len;
            }
        }
    }

    return s.substr(start, maxLen);
}

int main() {
    string input;
    cout << "Enter a string: ";
    cin >> input;
    string result = longestPalindrome(input);
    cout << "Longest Palindrome: " << result << endl;
    return 0;
}
```

This code implements a dynamic programming solution where `dp[i][j]` represents whether the substring from index `i` to index `j` (inclusive) is a palindrome or not. By utilizing this matrix, the algorithm checks all substrings of the input string to find the longest palindrome.

### 1. Algorithms & Data Structures (C++): Longest Palindromic Subsequence Problem

The Longest Palindromic Subsequence (LPS) problem is a classic problem in computer science and dynamic programming. In this problem, you're given a string, and you need to find the length of the longest subsequence (not necessarily contiguous) that is a palindrome. Here's how you can solve it in C++ using dynamic programming:

```cpp
#include <iostream>
#include <cstring>
using namespace std;

int longestPalindromeSubseq(string s) {
    int n = s.size();
    int dp[n][n];

    // Initialize the dp array with 1 for each single character
    for (int i = 0; i < n; i++)
        dp[i][i] = 1;

    // Build the dp array
    for (int len = 2; len <= n; len++) {
        for (int i = 0; i <= n - len; i++) {
            int j = i + len - 1;
            if (s[i] == s[j] && len == 2)
                dp[i][j] = 2;
            else if (s[i] == s[j])
                dp[i][j] = dp[i + 1][j - 1] + 2;
            else
                dp[i][j] = max(dp[i][j - 1], dp[i + 1][j]);
        }
    }

    // Return the length of the longest palindromic subsequence
    return dp[0][n - 1];
}

int main() {
    string s = "bbbab";
    cout << "Length of Longest Palindromic Subsequence: " << longestPalindromeSubseq(s) << endl;
    return 0;
}
```

In this code:

1. We create a 2D array `dp` to store the lengths of the longest palindromic subsequences for substrings of the given string `s`.
2. We initialize the diagonal of the `dp` array with 1 because each single character is a palindrome of length 1.
3. We then fill in the `dp` array in a bottom-up manner, starting from substrings of length 2 and gradually building up to the entire string.
4. At each step, we consider two cases:
   - If the characters at the two ends of the substring are the same, we can extend the palindromic subsequence by 2.
   - Otherwise, we choose the maximum of the lengths of the palindromic subsequences formed by excluding either the left or the right end character.
5. Finally, the length of the longest palindromic subsequence for the entire string is stored in `dp[0][n-1]`, where `n` is the length of the string.

This algorithm has a time complexity of O(n^2), where n is the length of the input string.

### 1. Algorithms & Data Structures (C++): Longest possible palindrome

To find the longest possible palindrome in a given string using C++, you can use dynamic programming. Here's a simple algorithm to achieve this:

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

string longestPalindrome(string s) {
    int n = s.length();
    if (n == 0) return "";

    vector<vector<bool>> dp(n, vector<bool>(n, false));
    int start = 0, maxLength = 1;

    // All substrings of length 1 are palindromes
    for (int i = 0; i < n; ++i)
        dp[i][i] = true;

    // Check for substrings of length 2
    for (int i = 0; i < n - 1; ++i) {
        if (s[i] == s[i + 1]) {
            dp[i][i + 1] = true;
            start = i;
            maxLength = 2;
        }
    }

    // Check for substrings of length greater than 2
    for (int len = 3; len <= n; ++len) {
        for (int i = 0; i < n - len + 1; ++i) {
            int j = i + len - 1;
            if (s[i] == s[j] && dp[i + 1][j - 1]) {
                dp[i][j] = true;
                start = i;
                maxLength = len;
            }
        }
    }
    return s.substr(start, maxLength);
}

int main() {
    string s = "babad";
    cout << "Longest palindrome: " << longestPalindrome(s) << endl;
    return 0;
}
```

This code defines a function `longestPalindrome` that takes a string `s` as input and returns the longest palindrome substring in that string. It uses dynamic programming to solve the problem in O(n^2) time complexity.

### 1. Algorithms & Data Structures (C++): Longest possible palindrome: Complexity analysis

To analyze the complexity of finding the longest possible palindrome in a string using C++, we can break it down into several steps:

1. **Generating Substrings**: We need to generate all possible substrings of the given string. Let's denote the length of the string as \( n \). Generating all substrings requires \( O(n^2) \) time complexity.

2. **Checking Palindrome**: For each substring, we need to check whether it is a palindrome or not. Checking if a string of length \( m \) is a palindrome can be done in \( O(m) \) time complexity.

3. **Finding the Longest**: Finally, we need to find the longest palindrome among all palindromic substrings. This can be done in linear time by keeping track of the longest palindrome found so far while iterating through the substrings.

Let's denote:

- \( n \) as the length of the input string.
- \( m \) as the length of the substring being checked for palindrome.

The overall time complexity can be summarized as follows:

- Generating Substrings: \( O(n^2) \)
- Checking Palindrome for each substring: \( O(n \cdot m) \) (In the worst case, \( m \) can be \( n \) itself)
- Finding the Longest: \( O(n) \)

So, the total time complexity is \( O(n^2) + O(n \cdot m) + O(n) \).

Now, let's discuss some optimizations:

1. **Manacher's Algorithm**: Manacher's algorithm can find all palindromic substrings in linear time. Using Manacher's algorithm, the time complexity for finding all palindromic substrings reduces to \( O(n) \).

2. **Dynamic Programming**: You can optimize the palindrome check by using dynamic programming to avoid redundant checks. The time complexity for palindrome check reduces to \( O(1) \) for each substring.

3. **Two-Pointer Technique**: While checking for palindromes, you can use a two-pointer technique to avoid unnecessary comparisons.

With these optimizations, the overall time complexity can be reduced significantly, making the algorithm more efficient.

### 1. Algorithms & Data Structures (C++): Longest substring without repeating characters

To find the longest substring without repeating characters in C++, you can use a sliding window approach. Here's an algorithm to achieve this:

```cpp
#include <iostream>
#include <unordered_set>
#include <string>

using namespace std;

int longestSubstringWithoutRepeatingChars(const string& s) {
    int n = s.length();
    unordered_set<char> charSet;
    int maxLen = 0;
    int i = 0, j = 0;

    while (i < n && j < n) {
        if (charSet.find(s[j]) == charSet.end()) {
            charSet.insert(s[j]);
            j++;
            maxLen = max(maxLen, j - i);
        } else {
            charSet.erase(s[i]);
            i++;
        }
    }

    return maxLen;
}

int main() {
    string s = "abcabcbb";
    cout << "Length of the longest substring without repeating characters: " 
         << longestSubstringWithoutRepeatingChars(s) << endl;
    return 0;
}
```

This code snippet defines a function `longestSubstringWithoutRepeatingChars` which takes a string `s` as input and returns the length of the longest substring without repeating characters.

Here's a brief overview of the algorithm:

- We use two pointers `i` and `j` to define a sliding window `[i, j)` that contains the substring without repeating characters.
- We use a set (unordered_set in C++) to store the characters in the current substring.
- If the character at index `j` is not in the set, we expand the window by moving `j` to the right and add the character to the set.
- If the character at index `j` is in the set, we shrink the window by moving `i` to the right and remove the character at index `i` from the set.
- We keep track of the maximum length of the substring without repeating characters encountered so far.
- Finally, we return the maximum length found.

This algorithm has a time complexity of O(n), where n is the length of the input string, as each character is visited at most twice (once by `i` and once by `j`).

### 1. Algorithms & Data Structures (C++): Longest Substring Without Repeating Characters - Dynamic Programming

To solve the "Longest Substring Without Repeating Characters" problem using dynamic programming in C++, you can utilize a hashmap to store the index of each character as you traverse the string. Here's a step-by-step approach:

1. Initialize a hashmap to store the last index of each character encountered.
2. Initialize two pointers, `start` and `end`, to track the current substring without repeating characters. Initialize `maxLength` to store the length of the longest substring.
3. Iterate through the string.
4. If the current character is not present in the hashmap or its last occurrence is before the `start` pointer, update the hashmap with the current index.
5. If the current character is already in the hashmap and its last occurrence is after or equal to the `start` pointer, update the `start` pointer to the index after the last occurrence of the character.
6. Update `maxLength` with the maximum of current `maxLength` and `end - start + 1`.
7. Return `maxLength` as the result.

Here's the C++ code implementing this algorithm:

```cpp
#include <unordered_map>
#include <algorithm>

int lengthOfLongestSubstring(string s) {
    // Initialize a hashmap to store the last index of each character
    unordered_map<char, int> charIndex;
    
    int start = 0; // Pointer to the start of the current substring
    int maxLength = 0; // Length of the longest substring without repeating characters
    
    for (int end = 0; end < s.size(); end++) {
        char currentChar = s[end];
        
        // If the character is found in the hashmap and its last occurrence is after or equal to the start pointer
        if (charIndex.find(currentChar) != charIndex.end() && charIndex[currentChar] >= start) {
            // Move the start pointer to the index after the last occurrence of the character
            start = charIndex[currentChar] + 1;
        }
        
        // Update the index of the current character in the hashmap
        charIndex[currentChar] = end;
        
        // Update maxLength with the maximum of current maxLength and end - start + 1
        maxLength = max(maxLength, end - start + 1);
    }
    
    return maxLength;
}
```

This solution has a time complexity of O(n), where n is the length of the input string, as we iterate through the string only once. The space complexity is O(min(m, n)), where m is the size of the character set (number of unique characters in the string) and n is the length of the input string.

### 1. Algorithms & Data Structures (C++): Longest Substring Without Repeating Characters - Sliding Window Method

The sliding window method is a popular technique used to solve problems involving arrays or strings by maintaining a window of elements that satisfy a certain condition. For the problem of finding the longest substring without repeating characters, the sliding window method is quite efficient.

Here's how you can implement the sliding window method in C++ to find the length of the longest substring without repeating characters:

```cpp
#include <iostream>
#include <unordered_set>
#include <string>

using namespace std;

int longestSubstringWithoutRepeatingChars(string s) {
    int n = s.length();
    int maxLength = 0;
    unordered_set<char> charSet;
    int left = 0, right = 0;

    while (right < n) {
        if (charSet.find(s[right]) == charSet.end()) {
            // If the current character is not in the set, add it to the set
            charSet.insert(s[right]);
            // Calculate the maximum length of the substring
            maxLength = max(maxLength, right - left + 1);
            // Move the right pointer to the next character
            right++;
        } else {
            // If the current character is in the set, remove characters from the left until no repeating characters are left
            charSet.erase(s[left]);
            // Move the left pointer to the next character
            left++;
        }
    }

    return maxLength;
}

int main() {
    string input = "abcabcbb";
    cout << "Length of the longest substring without repeating characters: "
         << longestSubstringWithoutRepeatingChars(input) << endl;
    return 0;
}
```

In this code:

- We maintain a sliding window `[left, right)` where `left` and `right` are the left and right pointers of the window.
- We use an unordered set to store characters in the current window.
- We iterate through the string with the `right` pointer, and for each character:
  - If it's not in the set, we add it to the set and update the maximum length if necessary.
  - If it's already in the set, we remove characters from the left until the current character is no longer in the set.
- We return the maximum length found.

This algorithm has a time complexity of O(n), where n is the length of the input string, because each character is visited at most twice by the two pointers.

### 1. Algorithms & Data Structures (C++): Longest substring without repeating characters: Complexity analysis

Sure, let's discuss the complexity analysis of finding the longest substring without repeating characters in a string using C++.

The problem can be solved using the sliding window technique. Here's a basic outline of the algorithm:

1. We use two pointers, `start` and `end`, to define the current window.
2. We move the `end` pointer to the right, expanding the window, until we find a repeating character.
3. Once we find a repeating character, we move the `start` pointer to the right until we remove the repeating character from the window.
4. Repeat steps 2 and 3 until we traverse the entire string.

Here's how we can analyze the time complexity:

- **Time Complexity**: O(n)
  - We traverse the string once with the `end` pointer, which gives us O(n).
  - While moving the `start` pointer, we can see that each character is visited at most twice (once by the `end` pointer and once by the `start` pointer).
  - So, the time complexity remains O(n).

- **Space Complexity**: O(min(n, m)), where n is the length of the input string and m is the size of the character set.
  - We use a hash set or an array of size 128 (assuming ASCII characters) to keep track of characters in the current window.
  - In the worst case, where all characters are unique, the size of the sliding window can grow up to the size of the input string, so the space complexity is O(n).
  - However, if the character set is limited (like ASCII characters), the space complexity becomes O(1).

Here's a simple C++ implementation:

```cpp
#include <iostream>
#include <unordered_set>
#include <algorithm>

using namespace std;

int lengthOfLongestSubstring(string s) {
    unordered_set<char> charSet;
    int maxLen = 0, start = 0, end = 0;
    
    while (end < s.length()) {
        if (charSet.find(s[end]) == charSet.end()) {
            charSet.insert(s[end]);
            maxLen = max(maxLen, end - start + 1);
            end++;
        } else {
            charSet.erase(s[start]);
            start++;
        }
    }
    
    return maxLen;
}

int main() {
    string s = "abcabcbb";
    cout << "Length of longest substring without repeating characters: " << lengthOfLongestSubstring(s) << endl;
    return 0;
}
```

This implementation has a time complexity of O(n) and a space complexity of O(min(n, m)).

### 1. Algorithms & Data Structures (C++): Make Palindrome

Sure, creating a palindrome from a given string involves appending characters to the end of the string such that it reads the same backward as forward. Here's a simple C++ function that takes a string as input and returns the palindrome formed by appending characters from the original string:

```cpp
#include <iostream>
#include <string>

using namespace std;

string makePalindrome(const string& str) {
    string palindrome = str;
    for (int i = str.length() - 2; i >= 0; --i) {
        palindrome += str[i];
    }
    return palindrome;
}

int main() {
    string input;
    cout << "Enter a string: ";
    getline(cin, input);

    string palindrome = makePalindrome(input);
    cout << "Palindrome: " << palindrome << endl;

    return 0;
}
```

This function iterates through the input string starting from the second last character (`str.length() - 2`) and appends each character to the original string, effectively creating the palindrome. Finally, it returns the palindrome string.

### 1. Algorithms & Data Structures (C++): Most Common Word

Certainly! Here's a C++ implementation to find the most common word in a given string using algorithms and data structures:

```cpp
#include <iostream>
#include <string>
#include <unordered_map>
#include <sstream>
#include <vector>
#include <algorithm>

using namespace std;

string mostCommonWord(string paragraph) {
    // Convert the paragraph to lowercase
    transform(paragraph.begin(), paragraph.end(), paragraph.begin(), ::tolower);
    
    // Replace non-alphabetic characters with spaces
    for (char& c : paragraph) {
        if (!isalpha(c)) {
            c = ' ';
        }
    }
    
    // Store the frequency of each word
    unordered_map<string, int> freqMap;
    istringstream iss(paragraph);
    string word;
    while (iss >> word) {
        freqMap[word]++;
    }
    
    // Find the word with maximum frequency
    string mostCommon;
    int maxFreq = 0;
    for (const auto& pair : freqMap) {
        if (pair.second > maxFreq) {
            mostCommon = pair.first;
            maxFreq = pair.second;
        }
    }
    
    return mostCommon;
}

int main() {
    string paragraph = "Bob hit a ball, the hit BALL flew far after it was hit.";
    cout << "Most common word: " << mostCommonWord(paragraph) << endl;
    return 0;
}
```

This program takes a paragraph as input, processes it to remove non-alphabetic characters and convert all words to lowercase, then it counts the frequency of each word using an unordered map. Finally, it finds the word with the maximum frequency and returns it as the most common word.

For the given example paragraph, the output would be:

```
Most common word: hit
```

Feel free to let me know if you need further explanation or assistance!

### 1. Algorithms & Data Structures (C++): Palindrome

Creating a palindrome checking algorithm involves examining whether a string reads the same forwards and backward. Here's a simple implementation in C++:

```cpp
#include <iostream>
#include <string>
#include <algorithm>

bool isPalindrome(const std::string& str) {
    // Get the length of the string
    int len = str.length();

    // Iterate over the first half of the string
    for (int i = 0; i < len / 2; ++i) {
        // Check if characters at corresponding positions from both ends are equal
        if (str[i] != str[len - i - 1]) {
            return false; // If not equal, not a palindrome
        }
    }
    return true; // If all characters match, it's a palindrome
}

int main() {
    std::string input;
    std::cout << "Enter a string: ";
    std::cin >> input;

    // Convert the input string to lowercase
    std::transform(input.begin(), input.end(), input.begin(), ::tolower);

    if (isPalindrome(input)) {
        std::cout << "Yes, it's a palindrome." << std::endl;
    } else {
        std::cout << "No, it's not a palindrome." << std::endl;
    }

    return 0;
}
```

This program first asks the user for a string input, converts it to lowercase (assuming case-insensitivity), and then checks whether the string is a palindrome using the `isPalindrome()` function. This function iterates through the string and compares characters from the beginning and the end of the string. If any characters don't match, it returns false; otherwise, it returns true.

### 1. Algorithms & Data Structures (C++): Palindrome Break

To implement a palindrome break algorithm in C++, you'll first need to define what exactly you mean by "palindrome break." If you're referring to breaking a given string into its constituent palindromes in all possible ways, you're essentially dealing with a problem of partitioning a string into palindromic substrings.

Here's a basic approach to solve this problem:

1. **Identify palindromes:** You need a function to check if a given substring is a palindrome. This can be done by iterating from both ends of the substring and comparing characters.

2. **Partitioning:** You need a recursive function to partition the string into palindromic substrings. At each step, you can choose to split the string at a particular index and check if both resulting substrings are palindromes.

Here's a simple implementation:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

bool isPalindrome(const string& str, int start, int end) {
    while (start < end) {
        if (str[start++] != str[end--]) {
            return false;
        }
    }
    return true;
}

void palindromePartitionHelper(const string& str, int start, vector<string>& current, vector<vector<string>>& result) {
    if (start == str.length()) {
        result.push_back(current);
        return;
    }

    for (int i = start; i < str.length(); ++i) {
        if (isPalindrome(str, start, i)) {
            current.push_back(str.substr(start, i - start + 1));
            palindromePartitionHelper(str, i + 1, current, result);
            current.pop_back();
        }
    }
}

vector<vector<string>> palindromePartition(const string& str) {
    vector<vector<string>> result;
    vector<string> current;
    palindromePartitionHelper(str, 0, current, result);
    return result;
}

int main() {
    string str = "aab";
    vector<vector<string>> partitions = palindromePartition(str);

    for (const auto& partition : partitions) {
        for (const string& palindrome : partition) {
            cout << palindrome << " ";
        }
        cout << endl;
    }

    return 0;
}
```

In this code:

- `isPalindrome` function checks if a given substring is a palindrome.
- `palindromePartitionHelper` recursively partitions the string into palindromic substrings and stores the partitions in the result vector.
- `palindromePartition` is the main function that initializes the process.
- In the `main` function, you can replace the string `str` with any string you want to find palindrome partitions for.

This code will print all possible partitions of the input string into palindromic substrings.

### 1. Algorithms & Data Structures (C++): Palindrome Number

Sure! A palindrome number is a number that remains the same when its digits are reversed. For example, 121, 1221, and 12321 are palindrome numbers.

Here's a simple C++ function to check if a given number is a palindrome:

```cpp
#include <iostream>

bool isPalindrome(int x) {
    // Handling negative numbers and numbers ending with 0, as they cannot be palindromes
    if (x < 0 || (x % 10 == 0 && x != 0))
        return false;
    
    int reversed = 0;
    while (x > reversed) {
        reversed = reversed * 10 + x % 10;
        x /= 10;
    }
    
    // If the number of digits is odd, we need to eliminate the middle digit
    return x == reversed || x == reversed / 10;
}

int main() {
    int num;
    std::cout << "Enter a number: ";
    std::cin >> num;
    
    if (isPalindrome(num))
        std::cout << num << " is a palindrome.\n";
    else
        std::cout << num << " is not a palindrome.\n";
    
    return 0;
}
```

In this code:

1. We handle negative numbers and numbers ending with 0 explicitly, as they cannot be palindromes.
2. We reverse the number by continuously extracting its last digit and adding it to the reversed number.
3. During the loop, when the original number becomes less than the reversed number, we stop because we have processed half of the digits (or the middle digit if the number has odd digits).
4. Finally, we compare the original number with the reversed number or the reversed number divided by 10 (to handle the middle digit for odd-length numbers), and return true if they are equal.

### 1. Algorithms & Data Structures (C++): Palindrome Partitioning

Palindrome partitioning is a classic problem in computer science that involves breaking a string into substrings such that each substring is a palindrome. Here's a C++ implementation using dynamic programming to solve the palindrome partitioning problem efficiently:

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <climits>

using namespace std;

bool isPalindrome(const string& s, int start, int end) {
    while (start < end) {
        if (s[start] != s[end])
            return false;
        start++;
        end--;
    }
    return true;
}

void partitionHelper(const string& s, int start, vector<string>& currentPartition, vector<vector<string>>& result) {
    if (start == s.length()) {
        result.push_back(currentPartition);
        return;
    }

    for (int i = start; i < s.length(); i++) {
        if (isPalindrome(s, start, i)) {
            currentPartition.push_back(s.substr(start, i - start + 1));
            partitionHelper(s, i + 1, currentPartition, result);
            currentPartition.pop_back();
        }
    }
}

vector<vector<string>> partition(const string& s) {
    vector<vector<string>> result;
    vector<string> currentPartition;
    partitionHelper(s, 0, currentPartition, result);
    return result;
}

int main() {
    string s = "aab";
    vector<vector<string>> partitions = partition(s);

    // Printing the partitions
    for (const auto& partition : partitions) {
        for (const auto& palindrome : partition) {
            cout << palindrome << " ";
        }
        cout << endl;
    }

    return 0;
}
```

In this implementation:

- `isPalindrome` function checks if a substring of the given string is a palindrome.
- `partitionHelper` is a recursive function that generates all possible palindrome partitions of the string `s` starting from the given index `start`.
- `partition` function initializes the necessary variables and calls the `partitionHelper` function to start the process.
- In the `main` function, you can change the input string `s` to any string you want to find its palindrome partitions.

This code will output all possible palindrome partitions of the input string `s`. Each partition is represented as a vector of strings.

### 1. Algorithms & Data Structures (C++): Palindrome String

Sure, here's a simple C++ function to check if a string is a palindrome:

```cpp
#include <iostream>
#include <string>
#include <algorithm>

bool isPalindrome(const std::string& str) {
    std::string reversed = str;
    std::reverse(reversed.begin(), reversed.end());
    return str == reversed;
}

int main() {
    std::string input;
    std::cout << "Enter a string: ";
    std::cin >> input;

    if (isPalindrome(input)) {
        std::cout << "Yes, it's a palindrome!" << std::endl;
    } else {
        std::cout << "No, it's not a palindrome." << std::endl;
    }

    return 0;
}
```

Explanation:

- The `isPalindrome` function takes a string as input and returns true if it's a palindrome, false otherwise.
- Inside the function, we create a copy of the input string called `reversed`.
- We then use the `std::reverse` function from the `<algorithm>` header to reverse the `reversed` string.
- Finally, we compare the original string with the reversed string and return true if they are equal.
- In the `main` function, we get input from the user, call the `isPalindrome` function, and print the result.

This code checks for palindromes considering case sensitivity. If you want to ignore case, you can convert the strings to lowercase (or uppercase) before comparing them.

### 1. Algorithms & Data Structures (C++): Palindromes

Sure, I can help you with that! Palindromes are strings that read the same forwards and backwards, like "radar" or "level".

Here's a simple C++ function to check if a given string is a palindrome:

```cpp
#include <iostream>
#include <string>
#include <algorithm>

bool isPalindrome(const std::string& str) {
    std::string reversed = str;
    std::reverse(reversed.begin(), reversed.end());
    return str == reversed;
}

int main() {
    std::string input;
    std::cout << "Enter a string: ";
    std::cin >> input;

    if (isPalindrome(input)) {
        std::cout << input << " is a palindrome." << std::endl;
    } else {
        std::cout << input << " is not a palindrome." << std::endl;
    }

    return 0;
}
```

This program first defines a function `isPalindrome()` which takes a string as input and returns true if it's a palindrome, and false otherwise. Inside the function, it creates a copy of the input string called `reversed`, reverses it using the `std::reverse()` function from the `<algorithm>` header, and then compares the original string with the reversed one. If they are equal, it returns true, otherwise false.

In the `main()` function, it prompts the user to enter a string, then calls `isPalindrome()` on that string and prints the result.

Feel free to ask if you need further clarification or have any questions!

### 1. Algorithms & Data Structures (C++): Palindromic Partitioning

Palindromic partitioning is a classic problem in computer science where you're tasked with dividing a string into as few substrings as possible, such that each substring is a palindrome. Here's a C++ implementation using dynamic programming to solve this problem efficiently:

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <climits>

using namespace std;

bool isPalindrome(const string& s, int start, int end) {
    while (start < end) {
        if (s[start++] != s[end--])
            return false;
    }
    return true;
}

int minPalPartition(const string& s) {
    int n = s.length();
    vector<vector<int>> dp(n, vector<int>(n, INT_MAX));

    for (int len = 1; len <= n; ++len) {
        for (int i = 0; i <= n - len; ++i) {
            int j = i + len - 1;
            if (isPalindrome(s, i, j))
                dp[i][j] = 0;
            else {
                for (int k = i; k < j; ++k) {
                    dp[i][j] = min(dp[i][j], 1 + dp[i][k] + dp[k + 1][j]);
                }
            }
        }
    }

    return dp[0][n - 1];
}

int main() {
    string s = "ababbbabbababa";
    cout << "Min cuts needed for Palindromic Partitioning: " << minPalPartition(s) << endl;
    return 0;
}
```

This code defines a function `minPalPartition` which takes a string `s` as input and returns the minimum number of partitions needed to make each partition a palindrome. The function `isPalindrome` checks if a given substring is a palindrome. The main function demonstrates how to use `minPalPartition` with a sample string.

### 1. Algorithms & Data Structures (C++): Paragraph Words Replacement

In C++, if you want to replace specific words in a paragraph, you can utilize various string manipulation techniques along with algorithms and data structures like `std::string`, `std::stringstream`, and `std::map`. Here's a basic example of how you can achieve this:

```cpp
#include <iostream>
#include <string>
#include <sstream>
#include <map>

// Function to replace words in a paragraph
std::string replaceWords(const std::string& paragraph, const std::map<std::string, std::string>& replacements) {
    std::stringstream ss(paragraph);
    std::string word;
    std::string replacedParagraph;

    while (ss >> word) {
        // Check if the word needs replacement
        if (replacements.find(word) != replacements.end()) {
            replacedParagraph += replacements.at(word) + " ";
        } else {
            replacedParagraph += word + " ";
        }
    }

    return replacedParagraph;
}

int main() {
    std::string paragraph = "This is a sample paragraph with some words.";
    std::map<std::string, std::string> replacements = {
        {"sample", "modified"},
        {"words", "terms"}
    };

    std::string modifiedParagraph = replaceWords(paragraph, replacements);
    std::cout << "Modified paragraph: " << modifiedParagraph << std::endl;

    return 0;
}
```

In this example:

1. We define a function `replaceWords` that takes the input paragraph and a map of replacements as arguments.
2. Inside the function, we use a `std::stringstream` to break the paragraph into words.
3. We iterate through each word and check if it needs replacement using the `replacements` map.
4. If a replacement is found, we append the replacement word to the `replacedParagraph`; otherwise, we append the original word.
5. Finally, we return the modified paragraph.

This code provides a basic framework for replacing words in a paragraph. You can extend and modify it according to your specific requirements, such as handling punctuation, case sensitivity, or multiple replacements of the same word.

### 1. Algorithms & Data Structures (C++): Paragraph Words Replacement - Trie Solution

In C++, you can efficiently solve the problem of replacing words in a paragraph using a Trie data structure. The idea is to build a Trie from the list of words you want to replace. Then, you traverse the paragraph word by word, checking if each word is in the Trie. If it is, you replace it with the corresponding word from the Trie.

Here's a basic implementation of this approach:

```cpp
#include <iostream>
#include <string>
#include <unordered_map>

using namespace std;

// Trie Node
struct TrieNode {
    unordered_map<char, TrieNode*> children;
    bool isEndOfWord;
    string replacement;

    TrieNode() : isEndOfWord(false), replacement("") {}
};

// Trie Class
class Trie {
public:
    Trie() {
        root = new TrieNode();
    }

    // Inserts a word into the trie.
    void insert(string word, string replacement) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                current->children[c] = new TrieNode();
            }
            current = current->children[c];
        }
        current->isEndOfWord = true;
        current->replacement = replacement;
    }

    // Returns true if the word is in the trie.
    bool search(string word) {
        TrieNode* node = searchNode(word);
        return node != nullptr && node->isEndOfWord;
    }

    // Returns the replacement for a word if it exists in the trie.
    string getReplacement(string word) {
        TrieNode* node = searchNode(word);
        return (node != nullptr && node->isEndOfWord) ? node->replacement : "";
    }

private:
    TrieNode* root;

    // Search a node which represents the given word.
    TrieNode* searchNode(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                return nullptr;
            }
            current = current->children[c];
        }
        return current;
    }
};

// Function to replace words in a paragraph using a Trie
string replaceWords(string paragraph, Trie& trie) {
    string result = "";
    string word = "";
    for (char c : paragraph) {
        if (c == ' ' || c == '.' || c == ',' || c == '!' || c == '?') {
            // Check if the word needs replacement
            string replacement = trie.getReplacement(word);
            if (!replacement.empty()) {
                result += replacement;
            } else {
                result += word;
            }
            result += c;
            word = "";
        } else {
            word += c;
        }
    }
    return result;
}

int main() {
    Trie trie;

    // Insert words and their replacements into the trie
    trie.insert("hello", "hi");
    trie.insert("world", "planet");

    string paragraph = "hello world! This is a test.";
    string replacedParagraph = replaceWords(paragraph, trie);

    cout << "Original Paragraph: " << paragraph << endl;
    cout << "Replaced Paragraph: " << replacedParagraph << endl;

    return 0;
}
```

This code defines a Trie data structure and a function `replaceWords` to replace words in a paragraph using the Trie. You can extend the Trie with more functionality if needed, like deleting words or handling different punctuation marks.

### 1. Algorithms & Data Structures (C++): parenthesis checking program

Certainly! Here's a simple C++ program to check if the parentheses in a given string are balanced or not using a stack data structure:

```cpp
#include <iostream>
#include <stack>
#include <string>

bool isBalanced(const std::string& str) {
    std::stack<char> stack;

    for (char ch : str) {
        if (ch == '(' || ch == '{' || ch == '[') {
            stack.push(ch);
        } else if (ch == ')' || ch == '}' || ch == ']') {
            if (stack.empty()) {
                return false; // Closing bracket with no matching opening bracket
            }

            char top = stack.top();
            stack.pop();

            // Check if the current closing bracket matches the top of the stack
            if ((ch == ')' && top != '(') ||
                (ch == '}' && top != '{') ||
                (ch == ']' && top != '[')) {
                return false;
            }
        }
    }

    // If stack is empty, all brackets are matched
    return stack.empty();
}

int main() {
    std::string expression;
    std::cout << "Enter an expression: ";
    std::cin >> expression;

    if (isBalanced(expression)) {
        std::cout << "Parentheses are balanced." << std::endl;
    } else {
        std::cout << "Parentheses are not balanced." << std::endl;
    }

    return 0;
}
```

This program defines a function `isBalanced()` that checks whether the parentheses in the input string are balanced or not. It uses a stack to keep track of opening parentheses encountered so far. If a closing parenthesis is encountered, it checks whether it matches the top of the stack (i.e., the last opening parenthesis). If the parentheses are balanced, the stack will be empty at the end.

### 1. Algorithms & Data Structures (C++): parenthesis checking program using Stack

Sure! Here's a simple C++ program to check if the parentheses in a given expression are balanced using a stack:

```cpp
#include <iostream>
#include <stack>
#include <string>

bool isBalanced(const std::string& expression) {
    std::stack<char> parentheses;

    for (char c : expression) {
        if (c == '(' || c == '[' || c == '{') {
            parentheses.push(c);
        } else if (c == ')' || c == ']' || c == '}') {
            if (parentheses.empty()) {
                return false; // More closing brackets than opening ones
            }

            char top = parentheses.top();
            parentheses.pop();

            if ((c == ')' && top != '(') || (c == ']' && top != '[') || (c == '}' && top != '{')) {
                return false; // Mismatched brackets
            }
        }
    }

    return parentheses.empty(); // Check if there are any remaining opening brackets
}

int main() {
    std::string expression;
    std::cout << "Enter an expression with parentheses: ";
    std::cin >> expression;

    if (isBalanced(expression)) {
        std::cout << "Parentheses are balanced.\n";
    } else {
        std::cout << "Parentheses are not balanced.\n";
    }

    return 0;
}
```

This program defines a function `isBalanced` which takes a string `expression` as input and returns `true` if the parentheses in the expression are balanced, and `false` otherwise. It uses a stack to keep track of the opening parentheses encountered so far. If a closing parenthesis is encountered, it checks whether the corresponding opening parenthesis is at the top of the stack. If not, it indicates that the parentheses are not balanced. Finally, the function returns `true` if the stack is empty at the end (i.e., all opening parentheses have been matched with closing ones).

The `main` function takes input from the user and calls the `isBalanced` function to check if the input expression has balanced parentheses.

### 1. Algorithms & Data Structures (C++): Parenthesis Matching

Sure, let's implement a simple algorithm in C++ to check if a given string of parentheses is balanced or not. The idea is to use a stack data structure to keep track of the opening parentheses encountered and then pop them off the stack when a closing parenthesis is encountered. If at any point, we encounter a closing parenthesis without a matching opening parenthesis, or if there are unmatched opening parentheses left at the end, then the string is not balanced.

Here's a sample implementation:

```cpp
#include <iostream>
#include <stack>
#include <string>

bool isBalanced(const std::string& str) {
    std::stack<char> parenthesesStack;

    for (char c : str) {
        if (c == '(' || c == '{' || c == '[') {
            // Push opening parentheses onto the stack
            parenthesesStack.push(c);
        } else if (c == ')' || c == '}' || c == ']') {
            // If closing parenthesis, check if there's a matching opening parenthesis
            if (parenthesesStack.empty()) {
                return false; // Unmatched closing parenthesis
            }

            // Pop the top element of the stack
            char top = parenthesesStack.top();
            parenthesesStack.pop();

            // Check if the popped opening parenthesis matches the current closing parenthesis
            if ((c == ')' && top != '(') || (c == '}' && top != '{') || (c == ']' && top != '[')) {
                return false; // Mismatched parentheses
            }
        }
    }

    // If stack is empty at the end, all parentheses were matched
    return parenthesesStack.empty();
}

int main() {
    std::string testString = "((()))"; // Balanced string
    if (isBalanced(testString)) {
        std::cout << "String is balanced." << std::endl;
    } else {
        std::cout << "String is not balanced." << std::endl;
    }

    return 0;
}
```

You can test this code with various strings containing parentheses to see if they're balanced or not. This algorithm has a time complexity of O(n), where n is the length of the input string.

### 1. Algorithms & Data Structures (C++): Pattern / String Matching

Pattern and string matching are fundamental tasks in computer science and are crucial in various applications such as text processing, data mining, and bioinformatics. In C++, you can implement several algorithms for pattern and string matching. Here are some common algorithms:

1. **Brute Force Method**: The simplest approach is to check every substring of the text against the pattern. This method has a time complexity of O((n - m + 1) * m), where n is the length of the text and m is the length of the pattern.

```cpp
#include <iostream>
#include <string>

using namespace std;

bool bruteForce(string text, string pattern) {
    int n = text.length();
    int m = pattern.length();

    for (int i = 0; i <= n - m; ++i) {
        int j;
        for (j = 0; j < m; ++j) {
            if (text[i + j] != pattern[j])
                break;
        }
        if (j == m) // Pattern found at index i
            return true;
    }
    return false; // Pattern not found
}

int main() {
    string text = "This is a sample text for pattern matching.";
    string pattern = "sample";
    if (bruteForce(text, pattern))
        cout << "Pattern found!" << endl;
    else
        cout << "Pattern not found." << endl;
    return 0;
}
```

2. **Knuth-Morris-Pratt (KMP) Algorithm**: This algorithm preprocesses the pattern to efficiently skip characters while searching. It has a time complexity of O(n + m), where n is the length of the text and m is the length of the pattern.

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

vector<int> computeLPS(string pattern) {
    int m = pattern.length();
    vector<int> lps(m, 0);
    int len = 0;
    int i = 1;

    while (i < m) {
        if (pattern[i] == pattern[len]) {
            len++;
            lps[i] = len;
            i++;
        } else {
            if (len != 0)
                len = lps[len - 1];
            else {
                lps[i] = 0;
                i++;
            }
        }
    }
    return lps;
}

bool KMP(string text, string pattern) {
    int n = text.length();
    int m = pattern.length();
    vector<int> lps = computeLPS(pattern);

    int i = 0, j = 0;
    while (i < n) {
        if (pattern[j] == text[i]) {
            j++;
            i++;
        }
        if (j == m) // Pattern found at index i-j
            return true;
        else if (i < n && pattern[j] != text[i]) {
            if (j != 0)
                j = lps[j - 1];
            else
                i = i + 1;
        }
    }
    return false; // Pattern not found
}

int main() {
    string text = "This is a sample text for pattern matching.";
    string pattern = "sample";
    if (KMP(text, pattern))
        cout << "Pattern found!" << endl;
    else
        cout << "Pattern not found." << endl;
    return 0;
}
```

These are just a couple of examples. There are many other algorithms like Boyer-Moore, Rabin-Karp, etc., each with its own advantages and use cases. The choice of algorithm depends on factors like the size of the text, characteristics of the pattern, and performance requirements.

### 1. Algorithms & Data Structures (C++): Print All Permutation of String

Certainly! Below is a C++ implementation to print all permutations of a given string using recursion:

```cpp
#include <iostream>
#include <string>
using namespace std;

void permute(string str, int l, int r) {
    if (l == r) {
        cout << str << endl;
        return;
    }
    for (int i = l; i <= r; i++) {
        swap(str[l], str[i]);
        permute(str, l + 1, r);
        swap(str[l], str[i]);
    }
}

void printAllPermutations(string str) {
    int n = str.length();
    permute(str, 0, n - 1);
}

int main() {
    string str;
    cout << "Enter a string: ";
    cin >> str;
    cout << "All permutations of the string are:" << endl;
    printAllPermutations(str);
    return 0;
}
```

This code defines a function `permute` which recursively generates all permutations of the string by swapping characters. Then, it defines `printAllPermutations` which sets up the initial call to `permute`. Finally, in `main`, it prompts the user to enter a string, then prints all permutations of that string.

### 1. Algorithms & Data Structures (C++): Print All Subsequences of String

To print all subsequences of a string in C++, you can use recursion. A subsequence of a string is a sequence that can be derived from the original string by deleting some or no elements without changing the order of the remaining elements.

Here's a C++ code to achieve this:

```cpp
#include <iostream>
#include <string>

using namespace std;

// Function to print all subsequences of a string
void printSubsequences(string str, string subsequence, int index) {
    // Base case: if index has reached the end of the string
    if (index == str.length()) {
        // Print the subsequence if it's not empty
        if (!subsequence.empty()) {
            cout << subsequence << endl;
        }
        return;
    }

    // Recursive call without including the current character
    printSubsequences(str, subsequence, index + 1);

    // Include the current character in the subsequence and call recursively
    printSubsequences(str, subsequence + str[index], index + 1);
}

int main() {
    string str;
    cout << "Enter a string: ";
    cin >> str;

    cout << "All subsequences of the string are: " << endl;
    printSubsequences(str, "", 0);

    return 0;
}
```

This code recursively generates all subsequences of the input string `str` by including or excluding each character at each step. The base case is when the index reaches the end of the string. We print the subsequence if it's not empty and return. Otherwise, we make two recursive calls: one without including the current character and one including the current character in the subsequence.

### 1. Algorithms & Data Structures (C++): Print Substring Without Using Extra Array

To print substrings without using an extra array in C++, you can use nested loops to iterate over the string and print each substring directly. Here's a simple example code:

```cpp
#include <iostream>
#include <string>

using namespace std;

void printSubstrings(const string& str) {
    int n = str.length();
    
    // Outer loop to iterate over each character in the string
    for (int i = 0; i < n; ++i) {
        // Inner loop to print substrings starting from character at index i
        for (int len = 1; len <= n - i; ++len) {
            // Print substring of length 'len' starting from index 'i'
            cout << str.substr(i, len) << endl;
        }
    }
}

int main() {
    string str = "hello";
    cout << "Substrings of \"" << str << "\":" << endl;
    printSubstrings(str);
    return 0;
}
```

This code defines a function `printSubstrings` that takes a string `str` as input and prints all possible substrings of `str`. The outer loop iterates over each character of the string, and the inner loop prints all substrings starting from that character by varying the length of the substring. The `substr` function is used to extract substrings from the original string.

### 1. Algorithms & Data Structures (C++): Program for Parenthesis Matching

Sure, here's a simple C++ program to check if the parentheses in a given string are properly matched using a stack data structure:

```cpp
#include <iostream>
#include <stack>
#include <string>

bool areParenthesesMatched(const std::string &expr) {
    std::stack<char> stack;
    
    for (char c : expr) {
        if (c == '(' || c == '[' || c == '{') {
            stack.push(c);
        } else if (c == ')' || c == ']' || c == '}') {
            if (stack.empty()) {
                return false;
            }
            char top = stack.top();
            stack.pop();
            if ((c == ')' && top != '(') ||
                (c == ']' && top != '[') ||
                (c == '}' && top != '{')) {
                return false;
            }
        }
    }
    
    return stack.empty();
}

int main() {
    std::string expression;
    std::cout << "Enter an expression with parentheses: ";
    std::cin >> expression;

    if (areParenthesesMatched(expression)) {
        std::cout << "Parentheses are properly matched.\n";
    } else {
        std::cout << "Parentheses are not properly matched.\n";
    }

    return 0;
}
```

This program uses a stack to keep track of opening parentheses encountered so far. When a closing parenthesis is encountered, it checks whether it matches the corresponding opening parenthesis at the top of the stack. If they match, the top element is popped from the stack, otherwise, the parentheses are not properly matched.

Hope this helps! Let me know if you have further questions!

### 1. Algorithms & Data Structures (C++): Rabin Karp Algorithm

The Rabin-Karp algorithm is a string searching algorithm that efficiently finds patterns within a text using hashing. It's particularly useful for searching multiple patterns in a single text or searching for a single pattern in multiple texts. Here's a brief overview of how it works:

1. **Hashing**: The algorithm begins by computing a hash value for the pattern to be searched and for each substring of the text with the same length as the pattern. This hash function should be chosen carefully to minimize the chance of hash collisions.

2. **Comparison**: Once the hash values are computed, the algorithm compares the hash value of the pattern with the hash values of the substrings of the text. If a match is found, it verifies the match by comparing the actual characters of the pattern with the corresponding characters in the substring.

3. **Rolling Hash**: To efficiently compute the hash values of the substrings, a rolling hash technique is often used. This allows the hash value of a substring to be computed in constant time based on the hash value of the previous substring.

4. **Handling Collisions**: Since hash collisions are possible, the algorithm should be designed to handle them. One common approach is to use a secondary verification step, where the algorithm checks if the pattern and substring match character by character if their hash values match.

Here's a simple implementation of the Rabin-Karp algorithm in C++:

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <cmath>

using namespace std;

const int prime = 101; // A prime number used in the hashing function

// Function to calculate the hash value of a substring
int calculateHash(const string& str, int start, int end) {
    int hash = 0;
    for (int i = start; i <= end; ++i) {
        hash += (int)str[i] * pow(prime, i - start);
    }
    return hash;
}

// Function to search for a pattern in a text using Rabin-Karp algorithm
void search(const string& text, const string& pattern) {
    int patternHash = calculateHash(pattern, 0, pattern.length() - 1);
    int patternLength = pattern.length();
    int textLength = text.length();

    for (int i = 0; i <= textLength - patternLength; ++i) {
        int textHash = calculateHash(text, i, i + patternLength - 1);
        if (textHash == patternHash) {
            bool match = true;
            for (int j = 0; j < patternLength; ++j) {
                if (text[i + j] != pattern[j]) {
                    match = false;
                    break;
                }
            }
            if (match) {
                cout << "Pattern found at index " << i << endl;
            }
        }
    }
}

int main() {
    string text = "ABABDABACDABABCABAB";
    string pattern = "ABABCABAB";

    cout << "Text: " << text << endl;
    cout << "Pattern: " << pattern << endl;

    search(text, pattern);

    return 0;
}
```

This is a basic implementation of the Rabin-Karp algorithm. In practice, you may want to optimize it further, especially in terms of choosing a good hash function and handling hash collisions efficiently. Additionally, there are more advanced variations of the algorithm that improve its performance in various scenarios.

### 1. Algorithms & Data Structures (C++): Ransom Note

Creating a ransom note algorithm involves determining if a given ransom note can be formed using the characters available in a given magazine text. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <unordered_map>

using namespace std;

bool canConstruct(string ransomNote, string magazine) {
    unordered_map<char, int> counts;
    
    // Count characters in magazine
    for (char c : magazine) {
        counts[c]++;
    }
    
    // Check if characters in ransomNote can be formed using magazine
    for (char c : ransomNote) {
        if (counts[c] == 0) {
            return false; // Character not available in magazine
        }
        counts[c]--; // Decrement count of character in magazine
    }
    
    return true;
}

int main() {
    string ransomNote = "aa";
    string magazine = "aab";
    
    if (canConstruct(ransomNote, magazine)) {
        cout << "Ransom note can be constructed from the magazine." << endl;
    } else {
        cout << "Ransom note cannot be constructed from the magazine." << endl;
    }
    
    return 0;
}
```

This code defines a function `canConstruct` that takes two strings, `ransomNote` and `magazine`, and checks if the characters in `ransomNote` can be formed using the characters in `magazine`. It uses an unordered map to count the occurrences of each character in the magazine. Then, it iterates through the characters in the ransom note, checking if each character is available in the magazine and decrementing its count accordingly. If any character is not available, it returns false; otherwise, it returns true.

### 1. Algorithms & Data Structures (C++): Redundant Paranthesis

In computer science, redundant parentheses refer to unnecessary or excessive use of parentheses in an expression, particularly in mathematical or logical expressions. This typically occurs when parentheses are used in a way that does not change the order of operations or the evaluation of the expression.

Here's a simple example in C++:

```cpp
#include <iostream>
#include <stack>
#include <string>

bool hasRedundantParentheses(const std::string& expression) {
    std::stack<char> s;

    for (char c : expression) {
        if (c == ')') {
            char top = s.top();
            s.pop();

            bool redundant = true;
            while (top != '(') {
                if (top == '+' || top == '-' || top == '*' || top == '/') {
                    redundant = false;
                }
                top = s.top();
                s.pop();
            }

            if (redundant)
                return true; // Found redundant parentheses
        } else {
            s.push(c);
        }
    }

    return false; // No redundant parentheses found
}

int main() {
    std::string expression = "((a+b))";
    if (hasRedundantParentheses(expression)) {
        std::cout << "Expression has redundant parentheses.\n";
    } else {
        std::cout << "Expression does not have redundant parentheses.\n";
    }
    return 0;
}
```

This code defines a function `hasRedundantParentheses` that checks if an expression has redundant parentheses. It uses a stack to keep track of opening parentheses encountered in the expression. When a closing parenthesis is encountered, it checks the contents of the stack to see if there are any operators between the opening and closing parentheses. If there are none, it considers the parentheses redundant. The main function demonstrates the usage of this function with a sample expression.

This is a basic approach, and in real-world applications, more sophisticated parsing techniques might be required to handle complex expressions correctly.

### 1. Algorithms & Data Structures (C++): Remove All Adjacent Duplicates

To remove all adjacent duplicates in a string using C++, you can utilize a stack data structure. The idea is to iterate through the string and keep track of characters in a stack. If the current character is the same as the top of the stack, we pop the character from the stack; otherwise, we push the character onto the stack. At the end, we construct the resulting string from the characters remaining in the stack.

Here's a C++ implementation:

```cpp
#include <iostream>
#include <stack>
#include <string>

using namespace std;

string removeDuplicates(string s) {
    stack<char> stk;
    
    for (char c : s) {
        if (!stk.empty() && stk.top() == c) {
            stk.pop(); // If current character is same as top of stack, pop it
        } else {
            stk.push(c); // Otherwise, push it onto the stack
        }
    }
    
    string result = "";
    while (!stk.empty()) {
        result = stk.top() + result;
        stk.pop();
    }
    
    return result;
}

int main() {
    string input = "abbaca";
    string result = removeDuplicates(input);
    cout << "Original string: " << input << endl;
    cout << "String after removing adjacent duplicates: " << result << endl;
    return 0;
}
```

In this implementation, we traverse through the string `s`. If the current character is equal to the top of the stack (and the stack is not empty), we pop the character from the stack. Otherwise, we push the character onto the stack. Finally, we construct the resulting string by popping characters from the stack and appending them to the result string.

### 1. Algorithms & Data Structures (C++): Remove All Adjacent Duplicates In String

To remove all adjacent duplicates in a string using C++, you can use a stack data structure. Here's a simple implementation:

```cpp
#include <iostream>
#include <stack>
#include <string>

using namespace std;

string removeDuplicates(string s) {
    stack<char> st;
    for (char c : s) {
        if (!st.empty() && st.top() == c) {
            st.pop(); // Remove the duplicate character
        } else {
            st.push(c); // Push non-duplicate characters onto the stack
        }
    }
    
    // Reconstruct the string from the stack
    string result = "";
    while (!st.empty()) {
        result = st.top() + result;
        st.pop();
    }
    
    return result;
}

int main() {
    string s = "abbaca";
    cout << "Original string: " << s << endl;
    cout << "String after removing adjacent duplicates: " << removeDuplicates(s) << endl;
    return 0;
}
```

This code defines a function `removeDuplicates` that takes a string `s` as input and returns the string with all adjacent duplicates removed. It iterates through the characters of the input string, maintaining a stack to keep track of the non-duplicate characters encountered so far. If the current character is the same as the character at the top of the stack, it indicates a duplicate, so the top element is removed. Otherwise, the current character is pushed onto the stack. Finally, the function reconstructs the string from the stack in reverse order.

### 1. Algorithms & Data Structures (C++): Remove Character Recursively

Certainly! To remove a specific character from a string recursively in C++, you can follow this approach:

```cpp
#include <iostream>
#include <string>

using namespace std;

// Function to remove a character recursively from a string
void removeChar(string &str, char ch, int index = 0) {
    // Base case: if the index exceeds the length of the string
    if (index >= str.length())
        return;

    // If the character at the current index matches the given character, remove it
    if (str[index] == ch) {
        str.erase(index, 1); // Remove 1 character starting from index
        // Note: After removal, the length of the string decreases by 1, so no need to increment index
    } else {
        // If the character at the current index does not match, move to the next index
        removeChar(str, ch, index + 1);
    }
}

int main() {
    string str = "hello world";
    char ch = 'o';

    cout << "Original string: " << str << endl;
    removeChar(str, ch);
    cout << "String after removing '" << ch << "': " << str << endl;

    return 0;
}
```

This code defines a function `removeChar` that takes a string `str`, a character `ch` to be removed, and an optional index (defaulted to 0) indicating the current position in the string. It recursively removes the character `ch` from the string `str`. The `main` function demonstrates its usage.

### 1. Algorithms & Data Structures (C++): Remove Consecutive Duplicates

To remove consecutive duplicates from a sequence (e.g., a string) in C++, you can iterate through the sequence and compare each element with the next one. If they are the same, skip the duplicate element. If they are different, keep the element. Here's a simple implementation:

```cpp
#include <iostream>
#include <string>

std::string removeConsecutiveDuplicates(const std::string& str) {
    std::string result;
    char prev = '\0'; // Initialize to null character

    for (char ch : str) {
        if (ch != prev) {
            result.push_back(ch);
            prev = ch;
        }
    }

    return result;
}

int main() {
    std::string str = "aaabbbcccdddeee";
    std::string result = removeConsecutiveDuplicates(str);
    std::cout << "Original string: " << str << std::endl;
    std::cout << "String with consecutive duplicates removed: " << result << std::endl;
    return 0;
}
```

This code defines a function `removeConsecutiveDuplicates` that takes a string as input and returns a new string with consecutive duplicates removed. In the `main` function, you can see an example usage. When you run this program, it will output:

```
Original string: aaabbbcccdddeee
String with consecutive duplicates removed: abcde
```

This code will work for any sequence of characters, not just strings. Just make sure to include the appropriate headers and adjust the data types if necessary.

### 1. Algorithms & Data Structures (C++): Remove duplicates

To remove duplicates from an array in C++, you can use various approaches depending on whether you want to preserve the original order of elements or not, and whether you can use additional data structures or not. Here's a common approach using a set to keep track of unique elements:

```cpp
#include <iostream>
#include <unordered_set>
#include <vector>

// Function to remove duplicates from an array
std::vector<int> removeDuplicates(const std::vector<int>& nums) {
    std::unordered_set<int> unique_nums;
    std::vector<int> result;

    for (int num : nums) {
        if (unique_nums.insert(num).second) {
            // If num is inserted successfully, it means it's unique
            result.push_back(num);
        }
    }

    return result;
}

int main() {
    std::vector<int> nums = {1, 2, 3, 3, 4, 5, 6, 6, 7, 8, 8, 9};
    std::vector<int> result = removeDuplicates(nums);

    std::cout << "Original Array: ";
    for (int num : nums) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    std::cout << "Array after removing duplicates: ";
    for (int num : result) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

This code defines a function `removeDuplicates` that takes a vector of integers and returns a new vector with duplicates removed. It uses an `unordered_set` to keep track of unique elements while iterating through the input array. If an element is not already present in the set, it is considered unique and added to the result vector.

This approach has a time complexity of O(n) due to the linear traversal of the input array, where n is the number of elements in the array. However, it uses additional space to store the unique elements in the set, resulting in a space complexity of O(n) in the worst case.

### 1. Algorithms & Data Structures (C++): Remove Vowels From a String

Certainly! Here's a C++ function to remove vowels from a string using basic algorithms and data structures:

```cpp
#include <iostream>
#include <string>
#include <unordered_set>

std::string removeVowels(const std::string& str) {
    std::string result;
    std::unordered_set<char> vowels = {'a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'};
    
    for (char ch : str) {
        if (vowels.find(ch) == vowels.end()) {
            result.push_back(ch);
        }
    }
    
    return result;
}

int main() {
    std::string input = "Hello, World!";
    std::cout << "Original string: " << input << std::endl;
    std::cout << "String without vowels: " << removeVowels(input) << std::endl;
    return 0;
}
```

This code defines a function `removeVowels` that takes a string as input and returns a new string with all vowels removed. It iterates through each character in the input string and checks if it's a vowel using an unordered set of vowels. If it's not a vowel, it's appended to the result string. Finally, the result string without vowels is returned.

In the `main` function, an example string "Hello, World!" is used to demonstrate the usage of the `removeVowels` function.

### 1. Algorithms & Data Structures (C++): Replace Character Recursively

Certainly! Below is a C++ function to replace all occurrences of a specified character in a string recursively:

```cpp
#include <iostream>
#include <string>

void replaceCharRecursively(std::string &str, char oldChar, char newChar, int index = 0) {
    if (index == str.length()) {
        return; // Base case: end of string
    }

    if (str[index] == oldChar) {
        str[index] = newChar; // Replace character if found
    }

    // Recur for the rest of the string
    replaceCharRecursively(str, oldChar, newChar, index + 1);
}

int main() {
    std::string str = "hello world";
    char oldChar = 'l';
    char newChar = 'z';

    replaceCharRecursively(str, oldChar, newChar);

    std::cout << "Modified string: " << str << std::endl;

    return 0;
}
```

This function `replaceCharRecursively` takes the input string `str`, the character to be replaced `oldChar`, and the character to replace it with `newChar`. It recursively traverses the string, replacing each occurrence of `oldChar` with `newChar`. Finally, in the `main()` function, you can see an example of usage where it replaces all occurrences of the character 'l' with 'z' in the string "hello world".

### 1. Algorithms & Data Structures (C++): Replace Characters

Certainly! Replacing characters in a string involves iterating through each character of the string and replacing certain characters with others. Here's a simple C++ function to achieve that:

```cpp
#include <iostream>
#include <string>

void replaceCharacters(std::string& str, char target, char replacement) {
    for (char& c : str) {
        if (c == target) {
            c = replacement;
        }
    }
}

int main() {
    std::string myString = "Hello, World!";
    char target = 'l';
    char replacement = 'z';
    
    std::cout << "Original string: " << myString << std::endl;
    
    replaceCharacters(myString, target, replacement);
    
    std::cout << "String after replacing '" << target << "' with '" << replacement << "': " << myString << std::endl;

    return 0;
}
```

This code defines a function `replaceCharacters` which takes a string reference `str`, a target character `target`, and a replacement character `replacement`. It iterates through each character of the string and replaces occurrences of the target character with the replacement character.

In the `main()` function, an example usage of this function is demonstrated by replacing all occurrences of character 'l' with 'z' in the string "Hello, World!". You can modify the `target` and `replacement` variables to replace different characters as needed.

### 1. Algorithms & Data Structures (C++): Reverse

Sure, here's an implementation of a function to reverse a string in C++:

```cpp
#include <iostream>
#include <string>

using namespace std;

void reverseString(string& s) {
    int left = 0;
    int right = s.length() - 1;
    
    while (left < right) {
        char temp = s[left];
        s[left] = s[right];
        s[right] = temp;
        left++;
        right--;
    }
}

int main() {
    string str = "hello";
    cout << "Original string: " << str << endl;
    
    reverseString(str);
    
    cout << "Reversed string: " << str << endl;
    
    return 0;
}
```

This code defines a function `reverseString` that takes a reference to a string and reverses it in place using a two-pointer approach. The `main` function demonstrates its usage by reversing the string "hello".

### 1. Algorithms & Data Structures (C++): Reverse A String

Sure! Here's a simple C++ code to reverse a string using the standard library:

```cpp
#include <iostream>
#include <string>

using namespace std;

string reverseString(const string& str) {
    string reversedStr = str;
    int n = str.length();
    for (int i = 0; i < n / 2; i++) {
        char temp = reversedStr[i];
        reversedStr[i] = reversedStr[n - i - 1];
        reversedStr[n - i - 1] = temp;
    }
    return reversedStr;
}

int main() {
    string input;
    cout << "Enter a string: ";
    getline(cin, input);
    string reversed = reverseString(input);
    cout << "Reversed string: " << reversed << endl;
    return 0;
}
```

This code defines a function `reverseString` that takes a string as input and returns its reversed version. It then prompts the user to enter a string, calls the `reverseString` function, and prints the reversed string.

### 1. Algorithms & Data Structures (C++): Reverse a String using Stack

Sure! Here's a C++ code to reverse a string using a stack:

```cpp
#include <iostream>
#include <stack>
#include <string>

using namespace std;

// Function to reverse a string using a stack
string reverseString(string str) {
    stack<char> s;

    // Push each character of the string onto the stack
    for (char c : str) {
        s.push(c);
    }

    string reversed = "";

    // Pop each character from the stack and append to the reversed string
    while (!s.empty()) {
        reversed += s.top();
        s.pop();
    }

    return reversed;
}

int main() {
    string input;
    cout << "Enter a string: ";
    getline(cin, input);

    string reversed = reverseString(input);
    cout << "Reversed string: " << reversed << endl;

    return 0;
}
```

In this code:

- We include necessary header files: `<iostream>` for input/output, `<stack>` for stack implementation, and `<string>` for string manipulation.
- We define a function `reverseString` that takes a string as input and returns its reverse.
- Inside the function, we use a stack to push each character of the input string onto it.
- Then, we pop each character from the stack and append it to a new string, effectively reversing the input string.
- Finally, we prompt the user to enter a string in the `main` function, call `reverseString` on it, and print the reversed string.

### 1. Algorithms & Data Structures (C++): Reverse Only Letters

To reverse only letters in a string in C++, you can follow these steps:

1. Create two pointers, one starting from the beginning of the string (`left`) and the other starting from the end (`right`).
2. Move `left` towards the right until you find a letter.
3. Move `right` towards the left until you find a letter.
4. Swap the characters at `left` and `right`.
5. Repeat steps 2-4 until `left` crosses `right`.

Here's a sample implementation:

```cpp
#include <iostream>
#include <string>
using namespace std;

bool isLetter(char c) {
    return (c >= 'a' && c <= 'z') || (c >= 'A' && c <= 'Z');
}

string reverseOnlyLetters(string s) {
    int left = 0;
    int right = s.size() - 1;

    while (left < right) {
        if (!isLetter(s[left])) {
            left++;
        } else if (!isLetter(s[right])) {
            right--;
        } else {
            // Swap only if both characters are letters
            swap(s[left], s[right]);
            left++;
            right--;
        }
    }

    return s;
}

int main() {
    string s = "a-bC-dEf-ghIj";
    cout << "Original string: " << s << endl;
    cout << "Reversed letters only: " << reverseOnlyLetters(s) << endl;
    return 0;
}
```

This code defines a function `reverseOnlyLetters` that takes a string as input and returns a string with only the letters reversed. The `isLetter` function checks if a character is a letter. In the `reverseOnlyLetters` function, it iterates through the string using two pointers (`left` and `right`) and swaps letters until `left` crosses `right`. Finally, in the `main` function, an example usage is shown.

### 1. Algorithms & Data Structures (C++): Reverse String

Certainly! Reversing a string is a common programming task and can be done in various ways. Here's a simple implementation in C++:

```cpp
#include <iostream>
#include <string>

using namespace std;

void reverseString(string& s) {
    int left = 0;
    int right = s.length() - 1;
    
    while (left < right) {
        // Swap characters at left and right indices
        char temp = s[left];
        s[left] = s[right];
        s[right] = temp;
        
        // Move towards the center
        left++;
        right--;
    }
}

int main() {
    string str = "Hello, world!";
    
    // Print original string
    cout << "Original string: " << str << endl;
    
    // Reverse the string
    reverseString(str);
    
    // Print reversed string
    cout << "Reversed string: " << str << endl;
    
    return 0;
}
```

This code defines a function `reverseString` that takes a reference to a string and reverses it in place. Then, in the `main` function, we demonstrate its usage by reversing the string "Hello, world!". Finally, we print both the original and reversed strings.

### 1. Algorithms & Data Structures (C++): Reverse Words in a String

To reverse words in a string using C++, you can follow these steps:

1. Split the string into words.
2. Reverse the order of the words.
3. Join the reversed words back into a string.

Here's a C++ implementation:

```cpp
#include <iostream>
#include <sstream>
#include <vector>
#include <algorithm>

std::string reverseWords(const std::string& s) {
    std::istringstream iss(s);
    std::vector<std::string> words;
    std::string word;

    // Split the string into words
    while (iss >> word) {
        words.push_back(word);
    }

    // Reverse the order of the words
    std::reverse(words.begin(), words.end());

    // Join the reversed words back into a string
    std::ostringstream oss;
    for (const auto& w : words) {
        oss << w << " ";
    }

    std::string reversedString = oss.str();
    // Remove the trailing space
    if (!reversedString.empty()) {
        reversedString.pop_back();
    }

    return reversedString;
}

int main() {
    std::string input = "Hello World!";
    std::cout << "Original string: " << input << std::endl;
    std::string reversed = reverseWords(input);
    std::cout << "Reversed string: " << reversed << std::endl;

    return 0;
}
```

This code will take an input string, split it into words, reverse the order of the words, and then join them back into a string. Finally, it prints the reversed string.

### 1. Algorithms & Data Structures (C++): Reversing a String

Reversing a string in C++ can be done in several ways, but one of the simplest approaches is to use the built-in `reverse` function from the `<algorithm>` header. Here's a basic example:

```cpp
#include <iostream>
#include <algorithm>
#include <string>

int main() {
    std::string str = "Hello, World!";
    
    // Using reverse function
    std::reverse(str.begin(), str.end());

    std::cout << "Reversed string: " << str << std::endl;

    return 0;
}
```

This code snippet demonstrates how to reverse a string using the `std::reverse` function from the `<algorithm>` header. After including the necessary headers, it declares a string `str` and then calls `std::reverse` with the iterators representing the beginning and end of the string. Finally, it prints the reversed string.

Another approach would be to reverse the string manually without using any library functions:

```cpp
#include <iostream>
#include <string>

void reverseString(std::string& str) {
    int left = 0;
    int right = str.length() - 1;

    while (left < right) {
        std::swap(str[left], str[right]);
        left++;
        right--;
    }
}

int main() {
    std::string str = "Hello, World!";
    
    // Using custom function
    reverseString(str);

    std::cout << "Reversed string: " << str << std::endl;

    return 0;
}
```

This code defines a function `reverseString` that takes a string reference and reverses it by swapping characters from the start and end of the string until they meet in the middle.

Both approaches achieve the same result, but using the `std::reverse` function is generally preferred as it's more concise and relies on standard library functionality.

### 1. Algorithms & Data Structures (C++): Rotate String

To rotate a string in C++, you can follow various approaches, but one common method is to use string manipulation techniques. Here's a simple implementation of a function to rotate a string by a given number of positions to the left:

```cpp
#include <iostream>
#include <string>

using namespace std;

string rotateString(const string& str, int k) {
    int n = str.length();
    k = k % n; // Handle cases where k is greater than string length

    // Rotate the string
    string rotated = str.substr(k) + str.substr(0, k);
    
    return rotated;
}

int main() {
    string str = "Hello World";
    int k = 3; // Number of positions to rotate left

    cout << "Original String: " << str << endl;
    cout << "Rotated String: " << rotateString(str, k) << endl;

    return 0;
}
```

This program defines a function `rotateString` that takes a string `str` and an integer `k` representing the number of positions to rotate the string to the left. Inside the function, it first calculates the effective rotation amount by taking the modulo of `k` with the length of the string. Then, it creates a new string by concatenating substrings of `str` - one starting from the `k`th position to the end, and another from the beginning to the `k`th position. Finally, it returns the rotated string.

In the `main` function, an example usage of this `rotateString` function is demonstrated. The original string "Hello World" is rotated by 3 positions to the left, and the result is printed to the console.

### 1. Algorithms & Data Structures (C++): Shortest palindrome

To find the shortest palindrome by appending characters to the beginning of a given string in C++, you can follow these steps:

1. Define a function that checks if a given string is a palindrome.
2. Start from the end of the given string and iterate backward.
3. For each position, check if the substring from the current position to the end is a palindrome.
4. If it's not a palindrome, add the character at the current position to the beginning of the string.
5. Repeat until you find the shortest palindrome.

Here's a sample implementation:

```cpp
#include <iostream>
#include <string>

using namespace std;

// Function to check if a string is palindrome
bool isPalindrome(const string& str) {
    int left = 0;
    int right = str.length() - 1;
    while (left < right) {
        if (str[left] != str[right]) {
            return false;
        }
        left++;
        right--;
    }
    return true;
}

// Function to find the shortest palindrome by appending characters
string shortestPalindrome(const string& str) {
    int n = str.length();
    string shortestPalin = str;

    for (int i = n - 1; i >= 0; i--) {
        string suffix = str.substr(i);
        if (!isPalindrome(suffix)) {
            shortestPalin = str[i] + shortestPalin; // Add character to the beginning
        }
    }
    return shortestPalin;
}

int main() {
    string input;
    cout << "Enter a string: ";
    cin >> input;

    string shortest = shortestPalindrome(input);
    cout << "Shortest palindrome: " << shortest << endl;

    return 0;
}
```

This code will take a string as input and output the shortest palindrome obtained by appending characters to its beginning.

### 1. Algorithms & Data Structures (C++): Shortest palindrome: Complexity analysis

The problem of finding the shortest palindrome that can be obtained by adding characters to the end of a given string can be approached with a relatively efficient algorithm. Here's a common approach in C++:

```cpp
#include <iostream>
#include <string>

using namespace std;

string shortestPalindrome(string s) {
    int n = s.size();
    string rev = s;
    reverse(rev.begin(), rev.end());
    string temp = s + "#" + rev;
    
    int m = temp.size();
    vector<int> lps(m, 0);
    
    for (int i = 1; i < m; ++i) {
        int j = lps[i - 1];
        while (j > 0 && temp[i] != temp[j])
            j = lps[j - 1];
        if (temp[i] == temp[j])
            ++j;
        lps[i] = j;
    }
    
    return rev.substr(0, n - lps[m - 1]) + s;
}

int main() {
    string s = "abcd";
    cout << shortestPalindrome(s) << endl; // Output: "dcbabcd"
    return 0;
}
```

This algorithm achieves linear time complexity O(n), where n is the length of the input string. Here's a breakdown of the complexity analysis:

1. **Reversal**: Reversing the input string `s` takes O(n) time, where n is the length of the string.
2. **Building the New String**: Creating the new string `temp` by concatenating `s`, a special character (`#`), and the reversed string `rev` takes O(n) time.
3. **Building the LPS (Longest Prefix Suffix) Array**: Constructing the LPS array for the string `temp` takes O(n) time. This is because it involves iterating through the characters of `temp` once and updating the LPS values based on a while loop that runs in linear time.

Therefore, the overall time complexity of the algorithm is O(n), where n is the length of the input string `s`.

Space complexity analysis:

- The space complexity is also O(n) due to the creation of the `rev`, `temp`, and `lps` arrays, each of which requires linear space in relation to the size of the input string.

This algorithm efficiently solves the problem of finding the shortest palindrome by leveraging the KMP (Knuth-Morris-Pratt) algorithm for pattern searching, which allows it to achieve linear time complexity.

### 1. Algorithms & Data Structures (C++): Shortest Superstring

To solve the Shortest Superstring problem, you typically use a technique like greedy algorithm, dynamic programming, or even genetic algorithms. Here's a general approach using dynamic programming in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Function to calculate overlap between two strings
int calculateOverlap(const string& a, const string& b) {
    int maxOverlap = min(a.length(), b.length());
    for (int i = maxOverlap; i > 0; --i) {
        if (a.substr(a.length() - i) == b.substr(0, i)) {
            return i;
        }
    }
    return 0;
}

// Function to calculate the shortest superstring
string shortestSuperstring(const vector<string>& strings) {
    int n = strings.size();

    // table[i][j] stores the overlap of string i with string j
    vector<vector<int>> overlaps(n, vector<int>(n));

    // Calculate overlaps
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < n; ++j) {
            if (i != j) {
                overlaps[i][j] = calculateOverlap(strings[i], strings[j]);
            }
        }
    }

    // dp[mask][i] stores the shortest superstring length ending with string i and covers the strings in the mask
    vector<vector<int>> dp(1 << n, vector<int>(n, INT_MAX));
    vector<vector<int>> parent(1 << n, vector<int>(n, -1));

    for (int mask = 0; mask < (1 << n); ++mask) {
        for (int i = 0; i < n; ++i) {
            if ((mask & (1 << i)) == 0) continue;
            if (mask == (1 << i)) {
                dp[mask][i] = strings[i].length();
            } else {
                for (int j = 0; j < n; ++j) {
                    if ((mask & (1 << j)) && j != i) {
                        int prev_mask = mask ^ (1 << i);
                        int overlap = overlaps[j][i];
                        if (dp[prev_mask][j] + (int)strings[i].length() - overlap < dp[mask][i]) {
                            dp[mask][i] = dp[prev_mask][j] + (int)strings[i].length() - overlap;
                            parent[mask][i] = j;
                        }
                    }
                }
            }
        }
    }

    // Finding the optimal ending string
    int ending = min_element(dp[(1 << n) - 1].begin(), dp[(1 << n) - 1].end()) - dp[(1 << n) - 1].begin();

    // Constructing the shortest superstring
    string superstring = strings[ending];
    int mask = (1 << n) - 1;
    int prev = ending;
    while (mask > 0) {
        int cur = parent[mask][prev];
        if (cur == -1) break;
        superstring = strings[cur].substr(0, strings[cur].length() - overlaps[cur][prev]) + superstring;
        mask ^= (1 << prev);
        prev = cur;
    }

    return superstring;
}

int main() {
    vector<string> strings = {"abc", "bcd", "cde"};
    string superstring = shortestSuperstring(strings);
    cout << "Shortest superstring: " << superstring << endl;
    return 0;
}
```

This code defines a function `shortestSuperstring` which takes a vector of strings as input and returns the shortest superstring formed by concatenating all strings in the vector. It uses dynamic programming to efficiently find the shortest superstring. The `calculateOverlap` function calculates the overlap between two strings, and the main function demonstrates its usage.

### 1. Algorithms & Data Structures (C++): Smallest Distinct Window

The problem of finding the smallest window in a string that contains all distinct characters can be solved efficiently using a sliding window technique. Here's a basic outline of the algorithm in C++:

```cpp
#include <iostream>
#include <string>
#include <unordered_map>

using namespace std;

string smallestDistinctWindow(const string& str) {
    unordered_map<char, int> charCount;
    int distinctCount = 0;
    int minLength = INT_MAX;
    int start = 0;
    int startIndex = 0;

    for (int i = 0; i < str.length(); ++i) {
        char c = str[i];
        
        if (charCount[c] == 0) // New distinct character found
            distinctCount++;
        
        charCount[c]++;

        // Try to minimize the window by moving the start pointer
        while (charCount[str[start]] > 1) {
            charCount[str[start]]--;
            start++;
        }

        // Update minimum length if all distinct characters are present
        if (distinctCount == charCount.size() && i - start + 1 < minLength) {
            minLength = i - start + 1;
            startIndex = start;
        }
    }

    return str.substr(startIndex, minLength);
}

int main() {
    string str = "abaacabca";
    cout << "Smallest distinct window: " << smallestDistinctWindow(str) << endl;
    return 0;
}
```

Explanation:

- We use a sliding window approach where we maintain a window containing all the distinct characters of the string.
- We iterate through the string and maintain a count of each character in the window using a hashmap.
- When a new distinct character is encountered, we increment the distinct count.
- We adjust the window size by moving the start pointer until we have all distinct characters in the window.
- We keep track of the minimum length window that contains all distinct characters.
- Finally, we return the substring corresponding to the minimum length window.

This algorithm has a time complexity of O(n), where n is the length of the input string.

### 1. Algorithms & Data Structures (C++): Store All Subsequences of String

Certainly! You can use recursion to generate all subsequences of a string. A subsequence of a string is a sequence of characters derived from the original string by deleting zero or more characters without changing the relative order of the remaining characters. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

// Function to generate all subsequences of a string
void generateSubsequences(string str, int index, string subsequence, vector<string>& subsequences) {
    // Base case: if index has reached the end of the string
    if (index == str.length()) {
        // If subsequence is not empty, add it to the list of subsequences
        if (!subsequence.empty())
            subsequences.push_back(subsequence);
        return;
    }

    // Recursive call without including the character at index
    generateSubsequences(str, index + 1, subsequence, subsequences);

    // Recursive call including the character at index
    generateSubsequences(str, index + 1, subsequence + str[index], subsequences);
}

int main() {
    string str = "abc";
    vector<string> subsequences;

    generateSubsequences(str, 0, "", subsequences);

    // Displaying all subsequences
    cout << "All subsequences of \"" << str << "\" are:" << endl;
    for (const string& subseq : subsequences) {
        cout << subseq << endl;
    }

    return 0;
}
```

This code will generate and print all subsequences of the string "abc". You can replace "abc" with any other string you want to find subsequences for.

### 1. Algorithms & Data Structures (C++): String Hashing - Polynomial Hash Function

Polynomial hashing is a technique used in computer science to efficiently hash strings. It's particularly useful in scenarios where you need to compare or search for substrings within larger strings. The basic idea is to treat the string as a polynomial with each character's ASCII value acting as a coefficient.

Here's a simple implementation of a polynomial hashing function in C++:

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

const int p = 31; // A prime number for better distribution
const int m = 1e9 + 9; // A large prime number to avoid collisions

// Function to compute the hash of a string
long long computeHash(const string& s) {
    long long hash_value = 0;
    long long p_pow = 1;
    for (char c : s) {
        hash_value = (hash_value + (c - 'a' + 1) * p_pow) % m;
        p_pow = (p_pow * p) % m;
    }
    return hash_value;
}

// Function to compute the hash of a substring
long long substringHash(const string& s, int start, int length) {
    long long hash_value = 0;
    long long p_pow = 1;
    for (int i = start; i < start + length; ++i) {
        hash_value = (hash_value + (s[i] - 'a' + 1) * p_pow) % m;
        p_pow = (p_pow * p) % m;
    }
    return hash_value;
}

int main() {
    string str = "hello";
    cout << "Hash of 'hello': " << computeHash(str) << endl;

    string substr = "ell";
    cout << "Hash of 'ell' in 'hello': " << substringHash(str, 1, substr.length()) << endl;

    return 0;
}
```

In this implementation:

- We choose a prime number `p` (typically a small prime like 31) and another large prime `m` (close to 10^9) for modulo operation to avoid integer overflow and achieve better distribution.
- The `computeHash` function calculates the hash value of a given string by treating it as a polynomial with coefficients derived from the ASCII values of its characters.
- The `substringHash` function computes the hash of a substring within a string using the same polynomial hashing approach but with a specified start index and length.
- Finally, in the `main` function, we demonstrate how to compute the hash of a string and a substring.

Keep in mind that while polynomial hashing is efficient, collisions can still occur. Using a large prime `m` helps mitigate this, but it's not entirely foolproof. Additionally, be cautious when dealing with modulo arithmetic to avoid overflow issues.

### 1. Algorithms & Data Structures (C++): String Key Sort

Sorting strings based on keys is a fundamental task in programming, especially when working with data structures and algorithms. In C++, you can use various sorting algorithms to achieve this. Here's an example of how you can sort strings based on keys in C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

// Function to compare two strings based on keys
bool compareStrings(const std::string &s1, const std::string &s2) {
    // Compare based on the first character of each string
    return s1[0] < s2[0];
}

int main() {
    std::vector<std::string> strings = {"apple", "banana", "cat", "dog", "elephant"};

    // Sorting the strings based on keys using the compareStrings function
    std::sort(strings.begin(), strings.end(), compareStrings);

    // Printing the sorted strings
    for (const auto &str : strings) {
        std::cout << str << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this example:

- We define a comparison function `compareStrings` that compares two strings based on their keys (in this case, the first character of each string).
- We use `std::sort` to sort the vector of strings, passing the `compareStrings` function as the comparator.
- Finally, we print the sorted strings.

You can modify the `compareStrings` function to define more complex sorting criteria based on different keys within the strings. Additionally, you can use other sorting algorithms like `std::stable_sort`, `std::partial_sort`, etc., depending on your requirements.

### 1. Algorithms & Data Structures (C++): String Matching with Finite Automaton

String matching with finite automaton is a technique used to efficiently find occurrences of a pattern within a larger text. It involves constructing a finite automaton (FA) that represents the pattern, and then traversing the text with this automaton to identify matches. Here's a basic outline of the algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

const int MAX_CHAR = 256;

// Construct finite automaton for the pattern
vector<vector<int>> constructFA(const string& pattern) {
    int m = pattern.length();
    vector<vector<int>> FA(m + 1, vector<int>(MAX_CHAR, 0));

    // Initialize the initial state
    FA[0][pattern[0]] = 1;

    int lps = 0; // Longest prefix suffix

    // Fill the rest of the table
    for (int i = 1; i <= m; ++i) {
        for (int j = 0; j < MAX_CHAR; ++j) {
            FA[i][j] = FA[lps][j];
        }
        if (i < m) {
            FA[i][pattern[i]] = i + 1;
            lps = FA[lps][pattern[i]];
        }
    }

    return FA;
}

// Perform string matching using finite automaton
void matchPattern(const string& text, const string& pattern) {
    int n = text.length();
    int m = pattern.length();
    vector<vector<int>> FA = constructFA(pattern);

    int state = 0; // Initial state

    // Traverse the text with the finite automaton
    for (int i = 0; i < n; ++i) {
        state = FA[state][text[i]];
        if (state == m) {
            cout << "Pattern found at index " << i - m + 1 << endl;
        }
    }
}

int main() {
    string text = "AABAACAADAABAAABAA";
    string pattern = "AABA";

    cout << "Text: " << text << endl;
    cout << "Pattern: " << pattern << endl;

    matchPattern(text, pattern);

    return 0;
}
```

In this code:

- `constructFA` constructs the finite automaton based on the pattern.
- `matchPattern` traverses the text using the finite automaton and prints the indices where the pattern is found.

This algorithm has a time complexity of O(n + m * |Σ|), where n is the length of the text, m is the length of the pattern, and |Σ| is the size of the alphabet. It's efficient for large texts and patterns, especially when |Σ| is relatively small compared to n and m.

### 1. Algorithms & Data Structures (C++): String Normalisation

String normalization in the context of algorithms and data structures typically refers to transforming a string into a canonical form to facilitate comparison or processing. Here's how you might approach string normalization in C++:

```cpp
#include <iostream>
#include <string>
#include <algorithm>
#include <cctype>

// Function to normalize a string
std::string normalizeString(const std::string& str) {
    std::string normalizedStr = str;

    // Convert all characters to lowercase
    std::transform(normalizedStr.begin(), normalizedStr.end(), normalizedStr.begin(), ::tolower);

    // Remove leading and trailing whitespaces
    auto start = normalizedStr.find_first_not_of(" \t\n");
    auto end = normalizedStr.find_last_not_of(" \t\n");
    if (start != std::string::npos && end != std::string::npos) {
        normalizedStr = normalizedStr.substr(start, end - start + 1);
    } else {
        normalizedStr.clear(); // String is all whitespace
    }

    // Replace consecutive whitespaces with a single space
    auto new_end = std::unique(normalizedStr.begin(), normalizedStr.end(),
                               [](char a, char b) { return std::isspace(a) && std::isspace(b); });
    normalizedStr.erase(new_end, normalizedStr.end());

    return normalizedStr;
}

int main() {
    std::string input = "  Hello    World!   ";
    std::string normalized = normalizeString(input);
    std::cout << "Normalized string: " << normalized << std::endl;
    return 0;
}
```

Explanation:

1. **Lowercasing**: Convert all characters of the string to lowercase using `std::transform`.
2. **Whitespace removal**: Remove leading and trailing whitespaces using `find_first_not_of` and `find_last_not_of`.
3. **Consecutive whitespace removal**: Replace consecutive whitespaces with a single space using `std::unique`.

This approach normalizes the string by converting it to lowercase and removing unnecessary whitespaces, making it suitable for comparison and processing. You can extend or modify this function based on your specific requirements or language nuances.

### 1. Algorithms & Data Structures (C++): String Problems

Certainly! String manipulation is a common task in programming, and understanding algorithms and data structures in this context can be quite useful. Here are some common string problems along with their solutions in C++:

1. **Reverse a String**:

   ```cpp
   #include <iostream>
   #include <string>
   using namespace std;

   string reverseString(string s) {
       int left = 0, right = s.length() - 1;
       while (left < right) {
           swap(s[left], s[right]);
           left++;
           right--;
       }
       return s;
   }

   int main() {
       string s = "hello";
       cout << "Original: " << s << endl;
       cout << "Reversed: " << reverseString(s) << endl;
       return 0;
   }
   ```

2. **Check if a String is Palindrome**:

   ```cpp
   #include <iostream>
   #include <string>
   using namespace std;

   bool isPalindrome(string s) {
       int left = 0, right = s.length() - 1;
       while (left < right) {
           if (s[left] != s[right])
               return false;
           left++;
           right--;
       }
       return true;
   }

   int main() {
       string s = "madam";
       cout << "Is palindrome: " << isPalindrome(s) << endl;
       return 0;
   }
   ```

3. **Count the Number of Words in a String**:

   ```cpp
   #include <iostream>
   #include <string>
   #include <sstream>
   using namespace std;

   int countWords(string s) {
       stringstream ss(s);
       string word;
       int count = 0;
       while (ss >> word)
           count++;
       return count;
   }

   int main() {
       string s = "Hello world, how are you?";
       cout << "Number of words: " << countWords(s) << endl;
       return 0;
   }
   ```

4. **Check Anagrams**:

   ```cpp
   #include <iostream>
   #include <string>
   #include <algorithm>
   using namespace std;

   bool areAnagrams(string s1, string s2) {
       sort(s1.begin(), s1.end());
       sort(s2.begin(), s2.end());
       return s1 == s2;
   }

   int main() {
       string s1 = "listen";
       string s2 = "silent";
       cout << "Are anagrams: " << areAnagrams(s1, s2) << endl;
       return 0;
   }
   ```

5. **Find Substring in a String**:

   ```cpp
   #include <iostream>
   #include <string>
   using namespace std;

   int findSubstring(string s, string target) {
       size_t found = s.find(target);
       if (found != string::npos)
           return found;
       else
           return -1;
   }

   int main() {
       string s = "hello world";
       string target = "world";
       int index = findSubstring(s, target);
       if (index != -1)
           cout << "Substring found at index: " << index << endl;
       else
           cout << "Substring not found." << endl;
       return 0;
   }
   ```

These examples cover some common string manipulation tasks in C++. Let me know if you need further explanation or have other questions!

### 1. Algorithms & Data Structures (C++): String Reversal

Certainly! Reversing a string is a fundamental problem in computer science and can be implemented using various approaches. Here's a simple implementation in C++:

```cpp
#include <iostream>
#include <string>

// Function to reverse a string
std::string reverseString(const std::string& str) {
    std::string reversedStr;
    for (int i = str.length() - 1; i >= 0; --i) {
        reversedStr.push_back(str[i]);
    }
    return reversedStr;
}

int main() {
    std::string input;
    std::cout << "Enter a string: ";
    std::getline(std::cin, input);

    std::string reversed = reverseString(input);
    std::cout << "Reversed string: " << reversed << std::endl;

    return 0;
}
```

Explanation:

1. `reverseString` function takes a string as input and returns its reversed form.
2. It initializes an empty string `reversedStr` to store the reversed string.
3. It iterates through the input string `str` in reverse order using a for loop.
4. At each iteration, it appends the character at index `i` of the input string to the `reversedStr`.
5. Finally, it returns the `reversedStr`.
6. In the `main` function, the user is prompted to enter a string.
7. The `reverseString` function is called with the input string, and the reversed string is printed.

This is a basic implementation. There are more efficient ways to reverse a string, like using in-place reversal techniques or standard library functions.

### 1. Algorithms & Data Structures (C++): String subsequences

Certainly! In C++, you can find string subsequences using recursion. A subsequence of a string is a new string that is formed from the original string by deleting some (or none) of the characters without changing the relative order of the remaining characters. Here's a recursive approach to find all subsequences of a given string:

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

void findSubsequences(string s, int index, string current, vector<string> &subsequences) {
    // Base case: when index reaches the length of the string
    if (index == s.length()) {
        // Add the current subsequence to the list
        subsequences.push_back(current);
        return;
    }

    // Recursive case:
    // Include the character at index 'index' in the current subsequence
    findSubsequences(s, index + 1, current + s[index], subsequences);

    // Exclude the character at index 'index' from the current subsequence
    findSubsequences(s, index + 1, current, subsequences);
}

int main() {
    string s = "abc";
    vector<string> subsequences;
    findSubsequences(s, 0, "", subsequences);

    // Output all subsequences
    cout << "Subsequences of " << s << " are:" << endl;
    for (const auto &subsequence : subsequences) {
        cout << subsequence << endl;
    }

    return 0;
}
```

This code defines a function `findSubsequences` that recursively generates all subsequences of a given string `s`. The function maintains an index to keep track of the current character being considered. At each step, it decides whether to include or exclude the current character in the subsequence. The base case is when the index reaches the end of the string, at which point the current subsequence is added to the list of subsequences.

In the `main` function, we call `findSubsequences` with the initial parameters and then output all the generated subsequences. You can modify the `main` function to use any other string as input.

### 1. Algorithms & Data Structures (C++): String subsequences: Complexity analysis

When analyzing the complexity of algorithms for generating string subsequences in C++, we typically consider two main approaches: recursive and iterative. Let's break down the complexity analysis for each approach:

1. Recursive Approach:
   In the recursive approach, we generate subsequences by considering each character in the string either by including it in the subsequence or excluding it.

   ```cpp
   void generateSubsequences(string str, int index, string current = "") {
       if (index == str.length()) {
           // Base case: Print or process the current subsequence
           cout << current << endl;
           return;
       }

       // Include the current character
       generateSubsequences(str, index + 1, current + str[index]);

       // Exclude the current character
       generateSubsequences(str, index + 1, current);
   }
   ```

   Complexity Analysis:
   - Time Complexity: O(2^N), where N is the length of the input string. This is because for each character in the string, we have two choices: include it or exclude it.
   - Space Complexity: O(N) on the call stack, where N is the length of the input string. This is due to the recursive calls.

2. Iterative Approach:
   In the iterative approach, we use bit manipulation to generate all possible combinations of characters.

   ```cpp
   void generateSubsequences(string str) {
       int n = str.length();
       for (int i = 0; i < (1 << n); i++) {
           string subsequence = "";
           for (int j = 0; j < n; j++) {
               if (i & (1 << j))
                   subsequence += str[j];
           }
           // Process or print the current subsequence
           cout << subsequence << endl;
       }
   }
   ```

   Complexity Analysis:
   - Time Complexity: O(2^N * N), where N is the length of the input string. The outer loop runs 2^N times, and for each iteration, we need to iterate over the length of the string (N) to construct the subsequence.
   - Space Complexity: O(1), as we are not using any additional space proportional to the size of the input.

In summary, both approaches have exponential time complexity, which is inherent in the problem of generating all subsequences of a string. However, the iterative approach may have a slightly higher constant factor due to the nested loops. The choice between these approaches depends on factors such as ease of implementation and performance requirements.

### 1. Algorithms & Data Structures (C++): String Window

The String Window problem is a common algorithmic challenge where you're given two strings: a larger string (the "source") and a smaller string (the "target"). The task is to find the smallest substring in the source string that contains all characters from the target string. This problem can be efficiently solved using the sliding window technique.

Here's an outline of how you can solve this problem in C++:

```cpp
#include <iostream>
#include <unordered_map>

using namespace std;

string minWindow(string s, string t) {
    unordered_map<char, int> targetFreq;
    for (char c : t)
        targetFreq[c]++;

    int left = 0, right = 0;
    int minLen = INT_MAX;
    int minLeft = 0;
    int requiredChars = targetFreq.size();
    int formedChars = 0;
    unordered_map<char, int> windowFreq;

    while (right < s.length()) {
        char currentChar = s[right];
        windowFreq[currentChar]++;
        
        if (targetFreq.find(currentChar) != targetFreq.end() && windowFreq[currentChar] == targetFreq[currentChar]) {
            formedChars++;
        }

        // Try to minimize the window by moving the left pointer
        while (left <= right && formedChars == requiredChars) {
            int windowSize = right - left + 1;
            if (windowSize < minLen) {
                minLen = windowSize;
                minLeft = left;
            }

            char leftChar = s[left];
            windowFreq[leftChar]--;
            if (targetFreq.find(leftChar) != targetFreq.end() && windowFreq[leftChar] < targetFreq[leftChar]) {
                formedChars--;
            }
            left++;
        }

        right++;
    }

    return (minLen == INT_MAX) ? "" : s.substr(minLeft, minLen);
}

int main() {
    string source = "ADOBECODEBANC";
    string target = "ABC";
    cout << "Smallest window containing all characters: " << minWindow(source, target) << endl;
    return 0;
}
```

This implementation maintains two pointers, `left` and `right`, representing the current window. It also keeps track of the frequency of characters in the current window and the target string.

The algorithm iterates through the source string, expanding the window to the right until it contains all the characters from the target string. Then, it tries to minimize the window size by contracting the window from the left side while still maintaining all the required characters.

The time complexity of this solution is O(N), where N is the length of the source string, as we iterate through each character of the source string only once.

### 1. Algorithms & Data Structures (C++): Strings

Certainly! Strings in C++ can be manipulated using various algorithms and data structures. Here's a brief overview:

#### 1. String Class

C++ provides a built-in `string` class in the Standard Template Library (STL) for string manipulation. This class provides a wide range of functions for various string operations like concatenation, substring search, etc.

```cpp
#include <string>
using namespace std;

string str1 = "Hello";
string str2 = "World";
string result = str1 + " " + str2; // Concatenation
```

#### 2. String Manipulation Algorithms

There are several algorithms for manipulating strings, including:

- **Substring Search:** Finding one string within another.
- **String Reversal:** Reversing the characters in a string.
- **String Comparison:** Comparing two strings lexicographically.
- **String Tokenization:** Splitting a string into tokens based on delimiters.

#### 3. Regular Expressions

Regular expressions allow for sophisticated pattern matching within strings. C++ provides the `<regex>` library for regular expression support.

```cpp
#include <iostream>
#include <regex>
using namespace std;

int main() {
    string str = "Hello, World!";
    regex pattern("\\b(W\\w+)"); // Matches words starting with 'W'
    smatch matches;
    while (regex_search(str, matches, pattern)) {
        cout << matches.str() << endl;
        str = matches.suffix().str();
    }
    return 0;
}
```

#### 4. Trie

A Trie (prefix tree) is a tree-like data structure used to store a dynamic set of strings. It's particularly useful for efficient prefix matching and searching.

#### 5. Suffix Array and Suffix Tree

Suffix arrays and suffix trees are data structures used for string searching. They enable quick searching of substrings within a larger text.

#### 6. Rolling Hash

Rolling hash functions are used in algorithms like Rabin-Karp for efficient substring search.

#### 7. String Compression

Algorithms like Huffman coding or Run-Length Encoding are used to compress strings efficiently.

#### 8. Levenshtein Distance

Levenshtein Distance calculates the minimum number of edits required to transform one string into another. It's useful in spell checking and DNA sequencing.

#### 9. Knuth-Morris-Pratt Algorithm

KMP is used for pattern searching in strings. It utilizes a failure function to avoid unnecessary comparisons.

These are just a few examples of algorithms and data structures related to strings in C++. Depending on the specific problem you're dealing with, you may need to use one or more of these techniques to efficiently manipulate strings.

### 1. Algorithms & Data Structures (C++): Strings - Almost A Palindrome

In the problem "Almost A Palindrome," you're typically given a string and asked to determine whether it is almost a palindrome or not. An almost palindrome is a string that becomes a palindrome after removing just one character.

Here's a simple approach in C++ to solve this problem:

```cpp
#include <iostream>
#include <string>

using namespace std;

// Function to check if a string is a palindrome
bool isPalindrome(const string& str) {
    int left = 0;
    int right = str.length() - 1;
    
    while (left < right) {
        if (str[left] != str[right])
            return false;
        left++;
        right--;
    }
    return true;
}

// Function to check if a string is almost a palindrome
bool almostPalindrome(const string& str) {
    int left = 0;
    int right = str.length() - 1;
    
    while (left < right) {
        if (str[left] != str[right]) {
            // Check if removing either left or right character makes it a palindrome
            return isPalindrome(str.substr(left, right - left)) ||
                   isPalindrome(str.substr(left + 1, right - left));
        }
        left++;
        right--;
    }
    return true; // If the string is already a palindrome
}

int main() {
    string str;
    cout << "Enter a string: ";
    cin >> str;

    if (almostPalindrome(str))
        cout << "The string is almost a palindrome.\n";
    else
        cout << "The string is not almost a palindrome.\n";

    return 0;
}
```

Here, the `isPalindrome` function checks if a given string is a palindrome or not. The `almostPalindrome` function iterates through the string from both ends and checks if removing any one character would make it a palindrome. If removing either the left or right character would result in a palindrome, then the string is considered almost a palindrome.

### 1. Algorithms & Data Structures (C++): Strings - Valid Palindrome & Almost Palindrome

Validating palindromes and nearly-palindromes is a common task in string manipulation. Let's break down how you might implement functions in C++ to determine whether a given string is a valid palindrome or an "almost" palindrome, where an almost palindrome can be made into a palindrome by removing just one character.

Here's a basic approach for each:

### Valid Palindrome

A palindrome is a string that reads the same backward as forward. To check if a string is a valid palindrome, you can compare characters from both ends of the string and move towards the center, checking if the characters match.

```cpp
#include <iostream>
#include <cctype>

bool isPalindrome(const std::string& s) {
    int left = 0;
    int right = s.length() - 1;
    
    while (left < right) {
        while (left < right && !isalnum(s[left])) // Skip non-alphanumeric characters
            left++;
        while (left < right && !isalnum(s[right]))
            right--;
        
        if (tolower(s[left]) != tolower(s[right])) // Ignore case
            return false;
        
        left++;
        right--;
    }
    return true;
}

int main() {
    std::string str = "A man, a plan, a canal, Panama!";
    std::cout << "Is \"" << str << "\" a palindrome? " << std::boolalpha << isPalindrome(str) << std::endl;
    return 0;
}
```

### Almost Palindrome

For an almost palindrome, you can slightly modify the palindrome-checking logic. You iterate through the string, removing one character at a time and then checking if the resulting string is a valid palindrome.

```cpp
bool isAlmostPalindrome(const std::string& s) {
    int left = 0;
    int right = s.length() - 1;
    
    while (left < right) {
        if (tolower(s[left]) != tolower(s[right])) { // Ignore case
            // Try removing one character from the left side
            bool isPalindromeWithoutLeft = true;
            for (int i = left + 1, j = right; i < j; ++i, --j) {
                if (tolower(s[i]) != tolower(s[j])) {
                    isPalindromeWithoutLeft = false;
                    break;
                }
            }
            if (isPalindromeWithoutLeft) return true;
            
            // Try removing one character from the right side
            bool isPalindromeWithoutRight = true;
            for (int i = left, j = right - 1; i < j; ++i, --j) {
                if (tolower(s[i]) != tolower(s[j])) {
                    isPalindromeWithoutRight = false;
                    break;
                }
            }
            return isPalindromeWithoutRight;
        }
        left++;
        right--;
    }
    return true;
}

int main() {
    std::string str = "abca";
    std::cout << "Is \"" << str << "\" an almost palindrome? " << std::boolalpha << isAlmostPalindrome(str) << std::endl;
    return 0;
}
```

These functions provide a basic implementation of checking for valid palindromes and almost palindromes in C++. They ignore non-alphanumeric characters and are case-insensitive. You can further optimize or modify them based on specific requirements or constraints.

### 1. Algorithms & Data Structures (C++): Strings - Valid Palindrome & Almost Palindrome: Analyzing Space and Time Complexity

Sure, let's analyze the space and time complexity of two string-related problems: Valid Palindrome and Almost Palindrome, implemented in C++.

### Valid Palindrome

A palindrome is a string that reads the same forwards and backwards. For example, "level" and "racecar" are palindromes. The problem of determining whether a given string is a valid palindrome involves comparing characters from both ends of the string until the middle is reached.

Here's a simple C++ function to check if a string is a valid palindrome:

```cpp
#include <cctype>

bool isPalindrome(string s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        if (!isalnum(s[left])) {
            left++;
            continue;
        }
        if (!isalnum(s[right])) {
            right--;
            continue;
        }
        if (tolower(s[left]) != tolower(s[right])) {
            return false;
        }
        left++;
        right--;
    }
    return true;
}
```

#### Time Complexity

- **Best Case:** O(n), where n is the length of the string. This occurs when the string is a palindrome, and we only need to traverse half of the string.
- **Worst Case:** O(n), where n is the length of the string. In the worst case, we may have to traverse the entire string.

#### Space Complexity

- O(1), as we are not using any additional data structures that scale with the size of the input string.

### Almost Palindrome

An almost palindrome is a string that becomes a palindrome after removing at most one character. For example, "abca" and "racecars" are almost palindromes. The problem involves checking if a given string is almost a palindrome.

Here's a C++ function to solve this problem:

```cpp
bool isAlmostPalindrome(string s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        if (s[left] != s[right]) {
            // Try removing either the left or right character
            return isPalindrome(s.substr(left, right - left)) || isPalindrome(s.substr(left + 1, right - left));
        }
        left++;
        right--;
    }
    return true;
}
```

#### Time Complexity

- **Best Case:** O(n), where n is the length of the string. This occurs when the string is already a palindrome, and we only need to traverse half of the string.
- **Worst Case:** O(n), where n is the length of the string. In the worst case, we may have to check both possible substrings after removing one character.

#### Space Complexity

- O(n), where n is the length of the string. This is due to the substrings created during the recursive calls in the worst-case scenario.

These complexities give an understanding of how these algorithms perform as the input size increases.

### 1. Algorithms & Data Structures (C++): Strings and Arrays

Sure, let's delve into some common algorithms and data structures for strings and arrays in C++.

### Strings

1. **String Length**:
   - `string.length()` or `string.size()` returns the length of the string.
  
2. **String Concatenation**:
   - Use the `+` operator or `append()` function to concatenate strings.

3. **String Comparison**:
   - Use `==` operator for equality comparison.
   - Use `<`, `>`, `<=`, `>=` operators for lexicographical comparison.

4. **Substring**:
   - `substr(startingIndex, length)` extracts a substring starting from `startingIndex` with a length of `length`.

5. **String Search**:
   - `find(substring)` or `rfind(substring)` returns the index of the first or last occurrence of the substring, respectively.

6. **String Modification**:
   - Strings are mutable in C++, so you can modify characters directly.
   - `string[index] = newChar` to modify a character.

7. **String to Integer**:
   - Use `stoi(string)` to convert a string to an integer.

8. **Integer to String**:
   - Use `to_string(integer)` to convert an integer to a string.

### Arrays

1. **Array Declaration**:
   - Declare arrays using `dataType arrayName[arraySize]`.

2. **Array Initialization**:
   - Initialize arrays during declaration like `int arr[5] = {1, 2, 3, 4, 5}`.

3. **Accessing Elements**:
   - Use square brackets `[]` and the index to access elements, e.g., `arr[index]`.

4. **Array Traversal**:
   - Use loops like `for` or `while` to traverse through array elements.

5. **Array Sorting**:
   - Use `sort(arr, arr + size)` from the `<algorithm>` library for sorting arrays.

6. **Array Searching**:
   - For unsorted arrays, linear search through the array.
   - For sorted arrays, binary search can be used (`binary_search`, `lower_bound`, `upper_bound`).

7. **Array Modification**:
   - Arrays are mutable, so you can modify elements directly.

8. **Multidimensional Arrays**:
   - Declare as `dataType arrayName[rowSize][colSize]`.

These are fundamental operations and techniques, but there's much more to explore in both areas. Each operation or algorithm may have various implementations and optimizations depending on the specific problem you're tackling.

### 1. Algorithms & Data Structures (C++): Strings Searching Inside String

Searching for strings within strings is a common task in programming. One efficient way to accomplish this is by using algorithms like the Knuth-Morris-Pratt (KMP) algorithm or the Boyer-Moore algorithm. Here's an example of how you can implement string searching using the KMP algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

// Function to compute the longest prefix suffix array for the pattern
vector<int> computeLPS(const string& pattern) {
    int n = pattern.size();
    vector<int> lps(n, 0);
    int len = 0; // Length of the previous longest prefix suffix

    int i = 1;
    while (i < n) {
        if (pattern[i] == pattern[len]) {
            len++;
            lps[i] = len;
            i++;
        } else {
            if (len != 0) {
                len = lps[len - 1];
            } else {
                lps[i] = 0;
                i++;
            }
        }
    }
    return lps;
}

// Function to perform string search using KMP algorithm
vector<int> KMPSearch(const string& text, const string& pattern) {
    vector<int> result;
    int n = text.size();
    int m = pattern.size();
    
    if (m == 0) return result; // Empty pattern
    
    vector<int> lps = computeLPS(pattern);
    
    int i = 0; // index for text[]
    int j = 0; // index for pattern[]
    while (i < n) {
        if (pattern[j] == text[i]) {
            i++;
            j++;
        }
        if (j == m) {
            result.push_back(i - j);
            j = lps[j - 1];
        } else if (i < n && pattern[j] != text[i]) {
            if (j != 0)
                j = lps[j - 1];
            else
                i++;
        }
    }
    return result;
}

int main() {
    string text = "AABAACAADAABAABA";
    string pattern = "AABA";
    
    vector<int> occurrences = KMPSearch(text, pattern);
    
    if (occurrences.empty()) {
        cout << "Pattern not found in the text.\n";
    } else {
        cout << "Pattern found at positions: ";
        for (int pos : occurrences) {
            cout << pos << " ";
        }
        cout << endl;
    }
    
    return 0;
}
```

This code demonstrates how to find occurrences of a pattern within a text using the Knuth-Morris-Pratt algorithm. The `computeLPS` function computes the longest prefix suffix array for the pattern, which is then used in the `KMPSearch` function to efficiently match the pattern against the text.

### 1. Algorithms & Data Structures (C++): Strings: Longest Substring Without Repeating Characters

To find the longest substring without repeating characters in a given string using C++, you can use a sliding window approach along with a hash set to keep track of characters seen so far. Here's a sample implementation:

```cpp
#include <iostream>
#include <string>
#include <unordered_set>

using namespace std;

int lengthOfLongestSubstring(string s) {
    unordered_set<char> charSet;
    int maxLength = 0;
    int left = 0, right = 0;

    while (right < s.length()) {
        if (charSet.find(s[right]) == charSet.end()) {
            // If the current character is not in the set, add it to the set
            charSet.insert(s[right]);
            // Update the max length if needed
            maxLength = max(maxLength, right - left + 1);
            right++;
        } else {
            // If the current character is in the set, remove characters from the left
            // until the current character is no longer in the set
            charSet.erase(s[left]);
            left++;
        }
    }

    return maxLength;
}

int main() {
    string s = "abcabcbb"; // Example string
    int result = lengthOfLongestSubstring(s);
    cout << "Length of the longest substring without repeating characters: " << result << endl;
    return 0;
}
```

In this code:

- We maintain a sliding window `[left, right]` where `left` represents the start of the substring and `right` represents the end.
- We use an unordered set `charSet` to store the characters in the current substring.
- We iterate through the string `s`, moving the `right` pointer forward. If the character at the `right` pointer is not in the set, we add it to the set and update the maximum length. If it's already in the set, we remove characters from the left side of the window until the character at `right` is no longer in the set.
- At each step, we update the maximum length of the substring without repeating characters.
- Finally, we return the maximum length.

### 1. Algorithms & Data Structures (C++): Strings: Longest Substring Without Repeating Characters: Analyzing Space and Time Complexity

The problem of finding the longest substring without repeating characters is a classic algorithmic problem. Here's the general approach to solve it in C++ and then analyze its time and space complexity:

```cpp
#include <string>
#include <unordered_map>
#include <algorithm>

int lengthOfLongestSubstring(std::string s) {
    std::unordered_map<char, int> charIndexMap;
    int maxLength = 0;
    int start = 0;

    for (int i = 0; i < s.length(); ++i) {
        if (charIndexMap.find(s[i]) != charIndexMap.end()) {
            start = std::max(start, charIndexMap[s[i]] + 1);
        }
        charIndexMap[s[i]] = i;
        maxLength = std::max(maxLength, i - start + 1);
    }

    return maxLength;
}

int main() {
    std::string input = "abcabcbb";
    int longestLength = lengthOfLongestSubstring(input);
    std::cout << "Longest substring length: " << longestLength << std::endl;
    return 0;
}
```

### Time Complexity Analysis

- **Iterating through the string**: The algorithm traverses the input string once, so the time complexity for this step is O(n), where n is the length of the input string.
- **Operations within the loop**: Inside the loop, the operations are constant time. The lookup in the unordered_map is on average O(1).
- Overall, the time complexity of the algorithm is O(n).

### Space Complexity Analysis

- **unordered_map**: The space complexity is dominated by the unordered_map `charIndexMap`, which stores characters and their indices. In the worst case, all characters are unique, so the space complexity is O(n).
- Other than the unordered_map, the algorithm uses only a few integer variables, which are constant space.
- Therefore, the space complexity of the algorithm is O(n).

This algorithm provides an efficient solution to find the length of the longest substring without repeating characters, with linear time complexity and linear space complexity in terms of the input string length.

### 1. Algorithms & Data Structures (C++): Strings: Typed Out Strings

In the context of algorithms and data structures, the problem of "Typed Out Strings" typically involves generating or simulating the string that would be outputted by typing a given string. Here's a typical problem statement:

**Problem:**
You're given a string `s`, which represents characters typed on a keyboard. Some characters are letters (a-z) while others are a backspace character '#'. The backspace character deletes the preceding character. Your task is to simulate the string that would be output by typing the characters of `s`.

**Example:**

```
Input: s = "ab#c"
Output: "ac"

Input: s = "ab##c"
Output: "c"

Input: s = "a##c#"
Output: ""
```

**Approach:**
One common approach to solve this problem is to use a stack. You iterate through the string and maintain a stack. When you encounter a letter, you push it onto the stack. When you encounter a backspace character, you pop a character from the stack (if the stack is not empty). Finally, you return the contents of the stack as the result.

Here's a simple C++ implementation of this approach:

```cpp
#include <iostream>
#include <stack>
#include <string>

using namespace std;

string typedOutString(const string& s) {
    stack<char> typed;
    for (char c : s) {
        if (c == '#') {
            if (!typed.empty()) typed.pop();
        } else {
            typed.push(c);
        }
    }

    string result;
    while (!typed.empty()) {
        result = typed.top() + result;
        typed.pop();
    }
    return result;
}

int main() {
    cout << typedOutString("ab#c") << endl;   // Output: "ac"
    cout << typedOutString("ab##c") << endl;  // Output: "c"
    cout << typedOutString("a##c#") << endl;  // Output: ""
    return 0;
}
```

This code should give you a good starting point for solving typed out strings problems in C++.

### 1. Algorithms & Data Structures (C++): Strings: Typed Out Strings: Analyzing Space and Time Complexity

Analyzing the space and time complexity of algorithms is crucial for understanding their efficiency and scalability. Let's delve into the space and time complexity of a C++ algorithm for generating typed out strings.

Consider the problem of generating a string based on a given string and a sequence of key presses. For example, given the input string "abc" and the key presses "3#2#1", the output string would be "cba". Here, '#' represents a backspace.

Here's a simple algorithm in C++ to solve this problem:

```cpp
#include <iostream>
#include <stack>
#include <string>

std::string generateTypedOutString(const std::string& input, const std::string& keyPresses) {
    std::stack<char> typedString;

    for (char c : input) {
        typedString.push(c);
    }

    int backspaceCount = 0;
    for (char c : keyPresses) {
        if (c == '#') {
            if (!typedString.empty()) {
                typedString.pop();
            } else {
                backspaceCount++;
            }
        } else {
            if (backspaceCount > 0) {
                backspaceCount--;
            } else {
                typedString.push(c);
            }
        }
    }

    std::string result;
    while (!typedString.empty()) {
        result += typedString.top();
        typedString.pop();
    }

    // Reverse the string to get the correct order
    std::reverse(result.begin(), result.end());

    return result;
}

int main() {
    std::string input = "abc";
    std::string keyPresses = "3#2#1";

    std::cout << generateTypedOutString(input, keyPresses) << std::endl;

    return 0;
}
```

Now, let's analyze the space and time complexity of this algorithm:

**Time Complexity:**

- The algorithm iterates over the input string and the key presses once. Therefore, the time complexity is O(N + M), where N is the length of the input string and M is the length of the key presses.

**Space Complexity:**

- The space complexity is primarily determined by the stack used to simulate the typing process. In the worst case, the stack might contain all characters from the input string, leading to a space complexity of O(N), where N is the length of the input string. Additionally, there is a constant amount of extra space used for variables and the result string. Therefore, the overall space complexity is O(N).

### 1. Algorithms & Data Structures (C++): Strings(Character Arrays)

Certainly! Strings, represented as character arrays, are fundamental in C++ programming. They are sequences of characters terminated by a null character ('\0'). Here's a basic overview of handling strings in C++, including common operations and some essential data structures:

### Basic String Operations

1. **Initialization**:

   ```cpp
   char str[] = "Hello"; // Initializing a string
   char str2[20]; // Declaring an empty string with a capacity of 20 characters
   ```

2. **Input/Output**:

   ```cpp
   char str[50];
   cin >> str; // Input a string
   cout << str; // Output a string
   ```

3. **String Length**:

   ```cpp
   strlen(str); // Returns the length of the string
   ```

4. **String Comparison**:

   ```cpp
   strcmp(str1, str2); // Returns 0 if strings are equal, <0 if str1 is less than str2, >0 if str1 is greater
   ```

5. **String Concatenation**:

   ```cpp
   strcat(str1, str2); // Concatenates str2 to str1
   ```

6. **Substring**:
   Not a built-in function. Requires manual manipulation of character arrays.

7. **String Copy**:

   ```cpp
   strcpy(destination, source); // Copies source to destination
   ```

8. **String Reverse**:
   Not a built-in function. Requires manual manipulation of character arrays.

### Essential Data Structures

1. **Linked List of Characters**:

   ```cpp
   struct Node {
       char data;
       Node* next;
   };
   ```

2. **Dynamic Arrays of Characters**:

   ```cpp
   char* dynamicStr = new char[50]; // Dynamic array
   delete[] dynamicStr; // Freeing memory after use
   ```

3. **Stack & Queue of Characters**:
   Use STL's `stack` and `queue` templates.

### String Manipulation Libraries

1. **

```cpp
#include <cstring> // For C-style string manipulation functions
```

2. **`

```cpp
#include <string> // For C++ string class
```

### C++ String Class

C++ also provides a high-level string class (`std::string`) in the `<string>` header. It offers more features and is generally easier to use compared to C-style character arrays. Here's how to use it:

1. **Initialization**:

   ```cpp
   std::string str = "Hello";
   ```

2. **Input/Output**:

   ```cpp
   std::string str;
   std::cin >> str; // Input a string
   std::cout << str; // Output a string
   ```

3. **String Length**:

   ```cpp
   str.length(); // Returns the length of the string
   ```

4. **String Comparison**:

   ```cpp
   str1.compare(str2); // Returns 0 if strings are equal, <0 if str1 is less than str2, >0 if str1 is greater
   ```

5. **String Concatenation**:

   ```cpp
   str1 + str2; // Concatenates str2 to str1
   ```

6. **Substring**:

   ```cpp
   str.substr(startIndex, length); // Returns the substring starting from startIndex with given length
   ```

7. **String Copy**:

   ```cpp
   std::string newStr = str; // Copies str to newStr
   ```

8. **String Reverse**:
   Not directly available. Requires manual manipulation or using algorithms.

Using `std::string` is often preferred due to its safety features, dynamic memory management, and built-in functionalities, which save time and reduce the chance of errors compared to working with character arrays directly.

### 1. Algorithms & Data Structures (C++): Substring search algorithms: Applications of substring search

Substring search algorithms, such as the famous Knuth-Morris-Pratt (KMP) algorithm or the Boyer-Moore algorithm, find numerous applications in various domains. Here are some common applications:

1. **Text Search**: One of the most straightforward applications is searching for a pattern within a text. This could be finding occurrences of a word within a document, searching for a specific sequence of characters in a string, or identifying keywords in a large body of text.

2. **Text Editors and IDEs**: Substring search algorithms are fundamental in text editors and Integrated Development Environments (IDEs) for functionalities like finding occurrences of a string, highlighting matches, and implementing the "Find" or "Search" feature.

3. **Database Systems**: In database systems, substring search algorithms are used in queries involving pattern matching, such as finding records that contain a specific substring or pattern. This is essential for efficient searching in large databases.

4. **Bioinformatics**: In bioinformatics, substring search algorithms are used for DNA and protein sequence analysis. Researchers use these algorithms to search for specific patterns or motifs within genetic sequences, aiding in tasks like gene identification, sequence alignment, and similarity searching.

5. **Compiler Design**: Compilers and interpreters often use substring search algorithms during lexical analysis and parsing phases. These algorithms help in tokenization, identifying keywords, and recognizing patterns in the source code.

6. **Data Compression**: Substring search algorithms play a role in data compression techniques like Lempel-Ziv-Welch (LZW) compression, which relies on finding repeated patterns within the data and replacing them with shorter codes.

7. **Network Security**: In network security applications, substring search algorithms are used for intrusion detection, packet inspection, and identifying patterns in network traffic. For example, searching for specific signatures in network packets to detect malicious activities like viruses or denial-of-service attacks.

8. **Natural Language Processing (NLP)**: NLP tasks often involve searching for specific patterns or sequences of words within text data. Substring search algorithms can be used for tasks like named entity recognition, sentiment analysis, and text classification.

9. **Image Processing**: In image processing, substring search algorithms can be applied to find specific patterns or features within images. This is useful in tasks like object detection, image recognition, and medical image analysis.

10. **String Matching in Genetics and Proteomics**: Substring search algorithms are used to match sequences in genetics and proteomics research, aiding in tasks like identifying homologous sequences, detecting gene mutations, and predicting protein structures.

These applications demonstrate the versatility and importance of substring search algorithms across various fields of computer science and beyond.

### 1. Algorithms & Data Structures (C++): Substring search algorithms: Brute-force search implementation

Certainly! Below is a simple implementation of the brute-force substring search algorithm in C++:

```cpp
#include <iostream>
#include <string>

using namespace std;

// Brute-force substring search algorithm
int bruteForceSearch(const string& text, const string& pattern) {
    int n = text.length();
    int m = pattern.length();

    for (int i = 0; i <= n - m; ++i) {
        int j;
        for (j = 0; j < m; ++j) {
            if (text[i + j] != pattern[j])
                break;
        }
        if (j == m)
            return i; // Pattern found at index i
    }

    return -1; // Pattern not found
}

int main() {
    string text = "Hello, how are you?";
    string pattern = "how";

    int index = bruteForceSearch(text, pattern);

    if (index != -1)
        cout << "Pattern found at index " << index << endl;
    else
        cout << "Pattern not found" << endl;

    return 0;
}
```

In this code:

- `bruteForceSearch` function takes two strings: `text` (the text to be searched) and `pattern` (the substring to be found in the text).
- It iterates through each character in the `text`, comparing it with the corresponding character in the `pattern`.
- If a mismatch is found, it breaks out of the inner loop and moves to the next character in the `text`.
- If the entire `pattern` matches the substring starting at the current position in the `text`, it returns the index of the starting position of the found substring.
- If no match is found, it returns -1.

You can test this implementation with different strings for `text` and `pattern` to see how it works.

### 1. Algorithms & Data Structures (C++): Substring search algorithms: Knuth-Morris-Pratt algorithm

The Knuth-Morris-Pratt (KMP) algorithm is a substring search algorithm that efficiently finds all occurrences of a pattern string within a text string. It has a time complexity of O(n + m), where n is the length of the text string and m is the length of the pattern string. Here's how it works:

1. **Preprocessing (Building the "Partial Match" Table)**:
   - Create a "partial match" table (also known as the "failure function" or "prefix function") for the pattern string. This table helps in determining where to resume the search in the pattern string if a mismatch occurs.
   - The partial match table is an array that stores the length of the longest proper prefix of the pattern that is also a suffix of the pattern.

2. **Searching**:
   - Start matching characters of the text and the pattern from left to right.
   - If a mismatch occurs at position j in the pattern, use the partial match table to determine how many characters can be skipped in the pattern without rechecking characters already matched.
   - Update the position in the pattern to resume matching based on the value in the partial match table.
   - Continue this process until either the end of the text string is reached or a complete match is found.

Here's a simple implementation of the KMP algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

vector<int> buildPartialMatchTable(const string& pattern) {
    int m = pattern.size();
    vector<int> table(m, 0);
    int j = 0;
    
    for (int i = 1; i < m; ++i) {
        while (j > 0 && pattern[i] != pattern[j]) {
            j = table[j - 1];
        }
        if (pattern[i] == pattern[j]) {
            table[i] = ++j;
        }
    }
    
    return table;
}

void KMP(const string& text, const string& pattern) {
    int n = text.size();
    int m = pattern.size();
    vector<int> table = buildPartialMatchTable(pattern);
    int j = 0;
    
    for (int i = 0; i < n; ++i) {
        while (j > 0 && text[i] != pattern[j]) {
            j = table[j - 1];
        }
        if (text[i] == pattern[j]) {
            ++j;
        }
        if (j == m) {
            cout << "Pattern found at index " << i - m + 1 << endl;
            j = table[j - 1];
        }
    }
}

int main() {
    string text = "ABABDABACDABABCABAB";
    string pattern = "ABABCABAB";
    KMP(text, pattern);
    return 0;
}
```

This implementation demonstrates how to use the KMP algorithm to find occurrences of a pattern string within a text string. The `buildPartialMatchTable` function constructs the partial match table for the pattern string, and the `KMP` function performs the actual search using this table.

### 1. Algorithms & Data Structures (C++): Substring search algorithms: Knuth-Morris-Pratt algorithm implementation

Sure, here's a basic implementation of the Knuth-Morris-Pratt (KMP) algorithm in C++ for substring search:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

// Compute the longest prefix which is also a suffix for each prefix of the pattern
vector<int> computeLPS(const string& pattern) {
    int n = pattern.size();
    vector<int> lps(n, 0); // lps[i] will store the length of the longest proper prefix which is also suffix of pattern[0..i]
    int len = 0; // Length of the previous longest prefix suffix

    // Base case: lps[0] is always 0
    int i = 1;
    while (i < n) {
        if (pattern[i] == pattern[len]) {
            len++;
            lps[i] = len;
            i++;
        } else {
            if (len != 0) {
                len = lps[len - 1];
            } else {
                lps[i] = 0;
                i++;
            }
        }
    }
    return lps;
}

// KMP algorithm for substring search
void KMP(const string& text, const string& pattern) {
    int m = pattern.size();
    int n = text.size();
    vector<int> lps = computeLPS(pattern);

    int i = 0; // Index for text[]
    int j = 0; // Index for pattern[]

    while (i < n) {
        if (pattern[j] == text[i]) {
            j++;
            i++;
        }

        if (j == m) {
            cout << "Found pattern at index " << i - j << endl;
            j = lps[j - 1];
        } else if (i < n && pattern[j] != text[i]) {
            if (j != 0)
                j = lps[j - 1];
            else
                i++;
        }
    }
}

int main() {
    string text = "ABABDABACDABABCABAB";
    string pattern = "ABABCABAB";
    KMP(text, pattern);
    return 0;
}
```

This code defines the KMP algorithm along with a helper function `computeLPS` to compute the Longest Proper Prefix which is also a Suffix (LPS) array for a given pattern. The `KMP` function then performs the substring search using the computed LPS array.

Feel free to adjust the `text` and `pattern` strings in the `main` function to test different inputs.

### 1. Algorithms & Data Structures (C++): Substring search algorithms: Knuth-Morris-Pratt algorithm: Constructing the partial match table

In the Knuth-Morris-Pratt (KMP) algorithm, the partial match table (also known as the failure function or the "pi" function) is crucial for efficiently finding occurrences of a pattern within a text. Here's how you can construct the partial match table in C++:

```cpp
#include <iostream>
#include <vector>
#include <string>

// Function to construct the partial match table
std::vector<int> constructPartialMatchTable(const std::string& pattern) {
    int m = pattern.length();
    std::vector<int> pi(m); // Partial match table

    pi[0] = 0; // The first character always has no proper prefix

    int k = 0; // Length of the longest proper prefix of the substring [0...i]
    for (int i = 1; i < m; ++i) {
        while (k > 0 && pattern[k] != pattern[i]) {
            // If mismatch, update k to the longest proper prefix of pattern[0...k-1]
            k = pi[k - 1];
        }
        if (pattern[k] == pattern[i]) {
            // If pattern[i] matches pattern[k], increase k
            ++k;
        }
        pi[i] = k; // Assign k as the length of the longest proper prefix of pattern[0...i]
    }

    return pi;
}

int main() {
    std::string pattern = "ababaca";
    std::vector<int> pi = constructPartialMatchTable(pattern);

    // Print the partial match table
    std::cout << "Partial Match Table:" << std::endl;
    for (int i = 0; i < pattern.length(); ++i) {
        std::cout << pi[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

In this code:

1. `constructPartialMatchTable` is a function that takes the pattern as input and constructs the partial match table.
2. We initialize an empty vector `pi` to store the values of the partial match table.
3. We set `pi[0] = 0` because the first character of the pattern cannot have any proper prefix.
4. We iterate over the characters of the pattern starting from index 1 and calculate the values of `pi`.
5. Inside the loop, we update `k` based on the previous values of `pi` until we find the longest proper prefix of `pattern[0...i]`.
6. Finally, we return the constructed partial match table.

You can use this partial match table in the KMP algorithm to efficiently search for occurrences of the pattern within a text.

### 1. Algorithms & Data Structures (C++): Substring search algorithms: Naive Substring Search

In C++, the Naive Substring Search algorithm is one of the simplest substring search algorithms. It iterates through the given string and checks if the substring matches starting from each index. Below is a basic implementation:

```cpp
#include <iostream>
#include <string>

using namespace std;

// Naive substring search function
int naiveSearch(string txt, string pat) {
    int n = txt.length();
    int m = pat.length();

    for (int i = 0; i <= n - m; i++) {
        int j;

        // Check if the current substring matches the pattern
        for (j = 0; j < m; j++)
            if (txt[i + j] != pat[j])
                break;

        // If the inner loop completed without a break, it means we found a match
        if (j == m)
            return i;
    }
    return -1; // Return -1 if no match found
}

int main() {
    string txt = "AABAACAADAABAAABAA";
    string pat = "AABA";

    int index = naiveSearch(txt, pat);

    if (index != -1)
        cout << "Pattern found at index " << index << endl;
    else
        cout << "Pattern not found" << endl;

    return 0;
}
```

This code defines the `naiveSearch` function which takes the text (`txt`) and the pattern (`pat`) to search for. It iterates through the text and at each index, it checks if the pattern matches starting from that index. If a match is found, it returns the index where the pattern starts, otherwise, it returns -1 if the pattern is not found.

In the `main` function, an example usage is demonstrated with a text and a pattern. You can change the values of `txt` and `pat` to test with different strings and patterns.

### 1. Algorithms & Data Structures (C++): Substring search algorithms: Rabin-Karp algorithm

The Rabin-Karp algorithm is a string searching algorithm that is used to find a substring within a larger string using hashing. It's particularly useful when you need to search for multiple patterns in the same text efficiently. Here's a basic rundown of how it works:

1. **Preprocessing**: Compute the hash value of the pattern (substring) and the hash values of all substrings of the text with the same length as the pattern. This step takes \( O(m) \) time, where \( m \) is the length of the pattern.

2. **Search**: Slide the pattern over the text one by one and compute the hash value of the current substring of the text. If the hash value of the current substring matches the hash value of the pattern, compare the characters of the pattern and the current substring. If they match, perform a full comparison to confirm the match. This step takes \( O(n) \) time, where \( n \) is the length of the text.

The key idea behind the Rabin-Karp algorithm is to use hashing to quickly compare substrings. By comparing hash values instead of comparing the actual characters, we can avoid comparing every character of the substring with the pattern unless there is a potential match.

One thing to be careful about with Rabin-Karp is hash collisions. Since we're using hashing, it's possible for different substrings to have the same hash value. In such cases, we need to perform a full comparison to confirm the match.

Here's a simple implementation of the Rabin-Karp algorithm in C++:

```cpp
#include <iostream>
#include <string>

using namespace std;

const int prime = 101; // A prime number to compute hash

// Function to compute hash value of a string
int computeHash(string const& str, int len) {
    int hash = 0;
    for (int i = 0; i < len; ++i) {
        hash += str[i] * pow(prime, i);
    }
    return hash;
}

// Function to implement Rabin-Karp algorithm
void rabinKarp(string const& text, string const& pattern) {
    int n = text.length();
    int m = pattern.length();
    int patternHash = computeHash(pattern, m);
    int textHash = computeHash(text, m);

    for (int i = 0; i <= n - m; ++i) {
        if (patternHash == textHash) {
            int j;
            for (j = 0; j < m; ++j) {
                if (text[i + j] != pattern[j]) {
                    break;
                }
            }
            if (j == m) {
                cout << "Pattern found at index " << i << endl;
            }
        }
        if (i < n - m) {
            textHash = (prime * (textHash - text[i] * pow(prime, m - 1))) + text[i + m];
        }
    }
}

int main() {
    string text = "ABABDABACDABABCABAB";
    string pattern = "ABABCABAB";
    rabinKarp(text, pattern);
    return 0;
}
```

This implementation computes hash values using a rolling hash technique, which helps avoid recalculating hash values for each substring. However, it's important to note that this implementation doesn't handle hash collisions. In a real-world scenario, you would need to implement a more robust hashing scheme to handle collisions effectively.

### 1. Algorithms & Data Structures (C++): Substring search algorithms: Substring search algorithms comparison

When comparing substring search algorithms in terms of their efficiency and performance, several factors come into play, such as time complexity, space complexity, and practical performance under various conditions. Let's compare a few common substring search algorithms in C++:

1. **Brute Force Algorithm**:
   - Time Complexity: O(n*m) where n is the length of the text and m is the length of the pattern.
   - Space Complexity: O(1).
   - Description: This algorithm involves checking every possible position in the text to see if the pattern matches starting from that position. It's simple but not very efficient, especially for large texts or patterns.

2. **Knuth-Morris-Pratt (KMP) Algorithm**:
   - Time Complexity: O(n + m) where n is the length of the text and m is the length of the pattern.
   - Space Complexity: O(m).
   - Description: KMP preprocesses the pattern to efficiently skip characters in the text based on the matches or mismatches found so far. It avoids unnecessary comparisons by utilizing information about the pattern itself.

3. **Boyer-Moore Algorithm**:
   - Time Complexity: Best case O(n/m), worst case O(nm), where n is the length of the text and m is the length of the pattern.
   - Space Complexity: O(m).
   - Description: Boyer-Moore preprocesses the pattern and compares characters from right to left. It skips portions of the text by using a heuristic based on the mismatched character's last occurrence in the pattern.

4. **Rabin-Karp Algorithm**:
   - Time Complexity: O(n + m) average, worst case O(nm), where n is the length of the text and m is the length of the pattern.
   - Space Complexity: O(1).
   - Description: Rabin-Karp algorithm uses hashing to find matches between the pattern and substrings of the text. It's particularly useful when multiple patterns need to be searched in the same text.

5. **Finite Automaton Algorithm**:
   - Time Complexity: O(n + m) preprocessing, O(n) matching, where n is the length of the text and m is the length of the pattern.
   - Space Complexity: O(m*alphabet size).
   - Description: This algorithm constructs a finite automaton that represents all occurrences of the pattern in the text. It's efficient in practice but requires preprocessing of the pattern.

Choosing the best algorithm depends on the specific requirements of the application, such as the length of the text and pattern, the frequency of searches, and available memory. In general, Boyer-Moore, KMP, and Rabin-Karp are commonly used for substring search due to their efficiency in different scenarios.

### 1. Algorithms & Data Structures (C++): Substring search algorithms: Z Algorithm

The Z algorithm is an efficient string matching algorithm used to find occurrences of a pattern within a text. It preprocesses the pattern to construct a Z array, which contains information about the longest substring starting from each position that matches the prefix of the pattern. Here's how the Z algorithm works:

1. **Preprocessing**: Construct the Z array for the pattern.
2. **Searching**: Slide the pattern over the text and compare characters. If the Z value matches the length of the pattern, a match is found.

Here's a basic implementation of the Z algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

vector<int> calculateZ(const string& str) {
    int n = str.length();
    vector<int> Z(n);
    int left = 0, right = 0;

    for (int i = 1; i < n; ++i) {
        if (i > right) {
            left = right = i;
            while (right < n && str[right - left] == str[right]) {
                right++;
            }
            Z[i] = right - left;
            right--;
        } else {
            int k = i - left;
            if (Z[k] < right - i + 1) {
                Z[i] = Z[k];
            } else {
                left = i;
                while (right < n && str[right - left] == str[right]) {
                    right++;
                }
                Z[i] = right - left;
                right--;
            }
        }
    }
    return Z;
}

vector<int> search(const string& text, const string& pattern) {
    string concat = pattern + "$" + text;
    vector<int> Z = calculateZ(concat);
    vector<int> result;

    for (int i = pattern.length() + 1; i < concat.length(); ++i) {
        if (Z[i] == pattern.length()) {
            result.push_back(i - pattern.length() - 1);
        }
    }
    return result;
}

int main() {
    string text = "aabxaabxcaabxaabxay";
    string pattern = "aabx";

    vector<int> result = search(text, pattern);

    if (!result.empty()) {
        cout << "Pattern found at indices: ";
        for (int i : result) {
            cout << i << " ";
        }
        cout << endl;
    } else {
        cout << "Pattern not found." << endl;
    }

    return 0;
}
```

This code demonstrates how to use the Z algorithm to search for a pattern within a text. The `calculateZ` function computes the Z array for a given string, and the `search` function finds occurrences of a pattern within a text using the Z array. Finally, in the `main` function, an example text and pattern are provided, and the matches are printed out.

### 1. Algorithms & Data Structures (C++): Substring search algorithms: Z algorithm illustration

The Z algorithm is an efficient algorithm for finding all occurrences of a pattern \( P \) within a text \( T \). It preprocesses the pattern to construct a Z-array, which contains information about the longest substring starting from each position in the pattern that matches a prefix of the pattern itself. By comparing the Z-array of the pattern with the Z-array of the concatenation of the pattern and the text, we can efficiently find all occurrences of the pattern in the text.

Here's an illustration of the Z algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

vector<int> z_algorithm(const string& text, const string& pattern) {
    string concat = pattern + "$" + text;
    int n = concat.length();

    vector<int> z(n, 0);
    int l = 0, r = 0;

    for (int i = 1; i < n; ++i) {
        if (i <= r)
            z[i] = min(r - i + 1, z[i - l]);
        
        while (i + z[i] < n && concat[z[i]] == concat[i + z[i]])
            ++z[i];
        
        if (i + z[i] - 1 > r) {
            l = i;
            r = i + z[i] - 1;
        }
    }

    vector<int> matches;
    for (int i = pattern.length() + 1; i < n; ++i) {
        if (z[i] == pattern.length())
            matches.push_back(i - pattern.length() - 1);
    }

    return matches;
}

int main() {
    string text = "abxabcabcaby";
    string pattern = "abc";

    vector<int> occurrences = z_algorithm(text, pattern);

    if (occurrences.empty())
        cout << "Pattern not found in the text." << endl;
    else {
        cout << "Pattern found at positions: ";
        for (int pos : occurrences)
            cout << pos << " ";
        cout << endl;
    }

    return 0;
}
```

This code demonstrates the Z algorithm for substring search in C++. It takes a text and a pattern as input and finds all occurrences of the pattern within the text using the Z algorithm.

Here's a brief overview of how the algorithm works:

1. Concatenate the pattern and text with a unique separator (here, we use '$').
2. Initialize a Z-array of size \( n \), where \( n \) is the length of the concatenated string.
3. Initialize variables \( l \) and \( r \) to keep track of the current interval where the pattern matches a prefix.
4. Iterate through the concatenated string from index 1 to \( n - 1 \).
5. If the current index \( i \) is within the interval \([l, r]\), update \( z[i] \) with the minimum of \( r - i + 1 \) and \( z[i - l] \).
6. While the characters at indices \( z[i] \) and \( i + z[i] \) are the same, increment \( z[i] \).
7. Update \( l \) and \( r \) if the current index \( i + z[i] - 1 \) is beyond \( r \).
8. Finally, find occurrences of the pattern by checking for \( z[i] = \text{{pattern length}} \) for indices greater than the length of the pattern.

This algorithm has a time complexity of \( O(n + m) \), where \( n \) is the length of the text and \( m \) is the length of the pattern.

### 1. Algorithms & Data Structures (C++): Substring search algorithms: Z algorithm implementation

The Z algorithm is an efficient pattern matching algorithm used for substring search. It preprocesses the pattern and then scans the text once to find all occurrences of the pattern. Here's a simple implementation of the Z algorithm in C++:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

vector<int> z_algorithm(const string& text, const string& pattern) {
    string concat = pattern + "$" + text;
    int n = concat.length();
    int m = pattern.length();

    vector<int> z(n, 0);
    int l = 0, r = 0;
    for (int i = 1; i < n; ++i) {
        if (i <= r)
            z[i] = min(r - i + 1, z[i - l]);
        while (i + z[i] < n && concat[z[i]] == concat[i + z[i]])
            ++z[i];
        if (i + z[i] - 1 > r) {
            l = i;
            r = i + z[i] - 1;
        }
    }

    vector<int> occurrences;
    for (int i = m + 1; i < n; ++i) {
        if (z[i] == m)
            occurrences.push_back(i - m - 1);
    }

    return occurrences;
}

int main() {
    string text = "abxabcabcaby";
    string pattern = "abcab";
    
    vector<int> occurrences = z_algorithm(text, pattern);
    
    if (occurrences.empty()) {
        cout << "Pattern not found in text." << endl;
    } else {
        cout << "Pattern found at positions: ";
        for (int pos : occurrences) {
            cout << pos << " ";
        }
        cout << endl;
    }

    return 0;
}
```

This implementation calculates the Z array which represents the length of the longest substring starting from `i` that is also a prefix of the string. By comparing the Z values with the length of the pattern, you can identify the positions where the pattern occurs in the text.

### 1. Algorithms & Data Structures (C++): The Closing Parentheses Problem

The Closing Parentheses Problem is a classic problem in algorithms and data structures. It involves determining whether a given expression has properly matched opening and closing parentheses. This problem often arises in programming, especially when dealing with parsing and evaluating mathematical expressions.

Here's a simple approach to solving the Closing Parentheses Problem in C++ using a stack:

```cpp
#include <iostream>
#include <stack>
#include <string>

bool areParenthesesMatched(const std::string& expression) {
    std::stack<char> parenthesesStack;

    for (char ch : expression) {
        if (ch == '(') {
            parenthesesStack.push(ch);
        } else if (ch == ')') {
            if (parenthesesStack.empty()) {
                return false; // More closing parentheses than opening ones
            }
            parenthesesStack.pop();
        }
    }

    return parenthesesStack.empty(); // Check if all opening parentheses have been matched
}

int main() {
    std::string expression;
    std::cout << "Enter an expression with parentheses: ";
    std::getline(std::cin, expression);

    if (areParenthesesMatched(expression)) {
        std::cout << "Parentheses are properly matched." << std::endl;
    } else {
        std::cout << "Parentheses are not properly matched." << std::endl;
    }

    return 0;
}
```

In this code:

- We iterate through each character in the input expression.
- If we encounter an opening parenthesis '(', we push it onto the stack.
- If we encounter a closing parenthesis ')', we check if the stack is empty. If it is empty, there are more closing parentheses than opening ones, so the expression is invalid. Otherwise, we pop an opening parenthesis from the stack, indicating that it has been matched.
- Finally, we check if the stack is empty. If it is, all opening parentheses have been matched, and the expression is valid.

This solution has a time complexity of O(n), where n is the length of the expression, since we only need to iterate through the expression once.

### 1. Algorithms & Data Structures (C++): The Knuth Morris Pratt Algorithm

The Knuth-Morris-Pratt (KMP) algorithm is a string searching algorithm that efficiently finds occurrences of a pattern within a text. It's particularly useful when you want to find all occurrences of a pattern in a text without redundant comparisons.

Here's a basic explanation of the algorithm:

1. **Preprocessing (Building the Prefix Table):**
   - The KMP algorithm preprocesses the pattern to create a prefix table, also known as a failure function or longest proper prefix which is also a suffix (LPS) array. This table helps in determining where to resume searching in the text when a mismatch occurs.
   - The idea is to find the length of the longest proper prefix of each prefix of the pattern that is also a suffix.

2. **Searching:**
   - During the searching phase, KMP compares characters of the text and the pattern.
   - When a mismatch occurs, instead of shifting the pattern by one position, the algorithm utilizes the information from the prefix table to determine the maximum possible shift. This is where KMP gains its efficiency over naive algorithms like the brute-force method.

Here's a C++ implementation of the KMP algorithm:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

// Function to build the prefix table for the given pattern
vector<int> buildPrefixTable(const string& pattern) {
    int m = pattern.length();
    vector<int> prefixTable(m, 0);
    int j = 0;
    for (int i = 1; i < m; ) {
        if (pattern[i] == pattern[j]) {
            prefixTable[i] = j + 1;
            i++;
            j++;
        } else {
            if (j != 0) {
                j = prefixTable[j - 1];
            } else {
                prefixTable[i] = 0;
                i++;
            }
        }
    }
    return prefixTable;
}

// Function to perform pattern searching using KMP algorithm
void KMPSearch(const string& text, const string& pattern) {
    int n = text.length();
    int m = pattern.length();
    vector<int> prefixTable = buildPrefixTable(pattern);

    int i = 0, j = 0;
    while (i < n) {
        if (pattern[j] == text[i]) {
            i++;
            j++;
        }
        if (j == m) {
            cout << "Pattern found at index " << i - j << endl;
            j = prefixTable[j - 1];
        } else if (i < n && pattern[j] != text[i]) {
            if (j != 0)
                j = prefixTable[j - 1];
            else
                i++;
        }
    }
}

int main() {
    string text = "ABCABCABCABABCABABCABCABCABCABCABCAB";
    string pattern = "ABCAB";
    KMPSearch(text, pattern);
    return 0;
}
```

This code demonstrates a simple application of the KMP algorithm to find occurrences of a pattern in a given text. The `buildPrefixTable` function constructs the prefix table for the pattern, and `KMPSearch` utilizes this table to efficiently search for occurrences of the pattern within the text.

### 1. Algorithms & Data Structures (C++): The Problem of String Matching

String matching is a fundamental problem in computer science and has numerous applications, such as text processing, bioinformatics, and data mining. In C++, there are several algorithms and data structures commonly used to solve the string matching problem efficiently. Here's a brief overview of some popular techniques:

1. **Brute Force Algorithm**:
   - Iterate through the text and compare each substring of the text of length equal to the pattern's length with the pattern.
   - Time complexity: O((n - m + 1) * m), where n is the length of the text and m is the length of the pattern.

2. **Knuth-Morris-Pratt (KMP) Algorithm**:
   - Preprocess the pattern to construct a prefix function (also known as the failure function), which helps in avoiding unnecessary comparisons.
   - Time complexity: O(n + m), where n is the length of the text and m is the length of the pattern.

3. **Rabin-Karp Algorithm**:
   - Use hashing to compare the pattern with substrings of the text efficiently.
   - Time complexity: O(n + m), where n is the length of the text and m is the length of the pattern on average. Worst-case complexity can be O(n * m).

4. **Boyer-Moore Algorithm**:
   - Preprocess the pattern and utilize the "bad character" and "good suffix" heuristics to skip comparisons.
   - Time complexity: O(n + m), where n is the length of the text and m is the length of the pattern in the best and average cases. Worst-case complexity can be O(n * m).

5. **Finite Automaton Algorithm**:
   - Construct a finite automaton that represents the pattern and use it to efficiently search for occurrences of the pattern in the text.
   - Time complexity: O(n + m), where n is the length of the text and m is the length of the pattern.

6. **Suffix Trees and Suffix Arrays**:
   - Construct data structures like suffix trees or suffix arrays to efficiently search for patterns in the text.
   - Time complexity: O(n + m), where n is the length of the text and m is the length of the pattern.

Each of these techniques has its advantages and disadvantages depending on factors like the length of the text and pattern, the frequency of pattern searches, and the available memory. The choice of algorithm often depends on the specific requirements of the application.

### 1. Algorithms & Data Structures (C++): Tokenisation (using sstream)

Tokenization is a fundamental operation in parsing and analyzing text data. In C++, one common way to tokenize a string is by using `std::stringstream` from the `<sstream>` header. Here's how you can tokenize a string using `std::stringstream`:

```cpp
#include <iostream>
#include <sstream>
#include <string>
#include <vector>

// Function to tokenize a string
std::vector<std::string> tokenizeString(const std::string &str, char delimiter) {
    std::vector<std::string> tokens;
    std::stringstream ss(str);
    std::string token;
    
    while (std::getline(ss, token, delimiter)) {
        tokens.push_back(token);
    }
    
    return tokens;
}

int main() {
    std::string input = "Hello,World,Tokenization,Example";
    char delimiter = ',';
    
    // Tokenize the input string
    std::vector<std::string> tokens = tokenizeString(input, delimiter);
    
    // Print the tokens
    std::cout << "Tokens:\n";
    for (const auto &token : tokens) {
        std::cout << token << std::endl;
    }
    
    return 0;
}
```

In this example, `tokenizeString` function takes a string (`str`) and a delimiter character (`delimiter`). It uses `std::stringstream` to split the input string into tokens based on the delimiter. The tokens are stored in a vector of strings, which is returned at the end.

In the `main` function, an example input string `"Hello,World,Tokenization,Example"` and a comma (`,`) as the delimiter are used. The tokens are then printed out to demonstrate the tokenization process.

You can modify the delimiter to tokenize the string differently, such as by space, tab, or any other character.

### 1. Algorithms & Data Structures (C++): Tokenisation (using strtok)

Tokenization is the process of breaking a string into smaller parts called tokens. In C++, one common way to tokenize a string is by using the `strtok` function from the `<cstring>` header.

Here's a simple example of tokenization using `strtok`:

```cpp
#include <iostream>
#include <cstring>

int main() {
    // Input string
    char str[] = "Hello, world! This is a test.";

    // Delimiter
    const char delim[] = " ,.!";

    // Tokenize the string
    char *token = strtok(str, delim);

    // Iterate through tokens
    while (token != nullptr) {
        std::cout << token << std::endl;
        token = strtok(nullptr, delim);
    }

    return 0;
}
```

In this example:

- `str` is the string to be tokenized.
- `delim` is a string containing delimiter characters. Each character in this string is considered a delimiter, and any of these characters found in `str` will be used to split it into tokens.
- `strtok` is used to extract tokens from `str`. It takes two arguments: the string to tokenize (on the first call) and a string containing the delimiter characters. On subsequent calls, you pass `nullptr` instead of the string to tokenize, and `strtok` will continue tokenizing the same string from where it left off.
- The `while` loop iterates through each token, printing it out.

One thing to note is that `strtok` modifies the input string by replacing delimiter characters with null characters. If you need to preserve the original string, you should make a copy before tokenizing it.

Additionally, `strtok` is not thread-safe. If you're working in a multithreaded environment, you should consider using `strtok_r` (or `strtok_s` on Windows) which are reentrant versions of `strtok`.

### 1. Algorithms & Data Structures (C++): Unique Characters

Certainly! Implementing a function in C++ to determine whether a string has all unique characters is a common problem. Here's a simple approach using a boolean array to track character occurrences:

```cpp
#include <iostream>
#include <string>
#include <vector>

bool allUniqueCharacters(const std::string& str) {
    // Assuming ASCII characters (0-127), if the character set is different, you'd adjust this array size
    std::vector<bool> charSet(128, false);
    
    for (char c : str) {
        int val = static_cast<int>(c);
        if (charSet[val]) {
            return false; // If character already encountered, string doesn't have all unique characters
        }
        charSet[val] = true;
    }
    
    return true; // If loop completes, all characters are unique
}

int main() {
    std::string str = "abcdefg";
    if (allUniqueCharacters(str)) {
        std::cout << "All characters in \"" << str << "\" are unique." << std::endl;
    } else {
        std::cout << "Not all characters in \"" << str << "\" are unique." << std::endl;
    }
    return 0;
}
```

This code iterates through each character of the string and checks if it has been encountered before. If it has, it returns false, indicating that not all characters in the string are unique. Otherwise, it marks the character as encountered and continues. If the loop completes without returning false, it means all characters are unique, and it returns true.

### 1. Algorithms & Data Structures (C++): Unique Substring (Hashing)

Sure, I can guide you through creating an algorithm in C++ to find the length of the longest substring with unique characters using hashing.

Here's a basic approach using hashing:

1. Iterate through the given string, maintaining a sliding window.
2. Use a hash set or an array to keep track of the characters seen so far in the current window.
3. Whenever we encounter a character that is already present in the hash set, update the start index of the window to the next index of the repeating character.
4. Calculate the length of the current window and update the maximum length encountered so far.
5. Continue this process until the end of the string is reached.

Let's implement this:

```cpp
#include <iostream>
#include <unordered_set>
#include <algorithm>

using namespace std;

int longestUniqueSubstringLength(const string& str) {
    int n = str.length();
    int maxLength = 0;
    int start = 0;
    unordered_set<char> seenChars;

    for (int end = 0; end < n; end++) {
        char currentChar = str[end];
        if (seenChars.find(currentChar) != seenChars.end()) {
            // If the current character is already in the window,
            // move the start of the window to the next index of the repeating character.
            while (str[start] != currentChar) {
                seenChars.erase(str[start]);
                start++;
            }
            start++;
        } else {
            // If the current character is not in the window, add it to the set.
            seenChars.insert(currentChar);
        }
        // Update the maximum length encountered so far.
        maxLength = max(maxLength, end - start + 1);
    }

    return maxLength;
}

int main() {
    string str = "abcabcbb";
    cout << "Length of the longest substring with unique characters: " << longestUniqueSubstringLength(str) << endl;
    return 0;
}
```

This code will output the length of the longest substring with unique characters in the given string "abcabcbb", which is 3 (substring "abc"). You can replace the sample string with any other string to test the function.

### 1. Algorithms & Data Structures (C++): Unique Substring Implementation

Implementing an algorithm to find unique substrings in a string involves iterating through all possible substrings and storing them in a data structure that maintains uniqueness, like a set. Here's a simple implementation in C++:

```cpp
#include <iostream>
#include <unordered_set>
#include <string>

std::unordered_set<std::string> uniqueSubstrings(const std::string& str) {
    std::unordered_set<std::string> uniqueSubs;
    int n = str.length();

    // Iterate over all possible substrings
    for (int len = 1; len <= n; ++len) {
        // Generate substrings of length 'len'
        for (int start = 0; start <= n - len; ++start) {
            std::string substring = str.substr(start, len);
            uniqueSubs.insert(substring);
        }
    }

    return uniqueSubs;
}

int main() {
    std::string input;
    std::cout << "Enter a string: ";
    std::cin >> input;

    std::unordered_set<std::string> result = uniqueSubstrings(input);

    std::cout << "Unique Substrings:\n";
    for (const auto& s : result) {
        std::cout << s << "\n";
    }

    return 0;
}
```

This code defines a function `uniqueSubstrings` that takes a string `str` as input and returns a set of unique substrings. It generates all possible substrings of `str` using nested loops, inserts them into an `unordered_set`, which automatically ensures uniqueness, and then returns the set.

In the `main` function, it prompts the user to enter a string, calls `uniqueSubstrings`, and prints out the unique substrings.

Remember that this approach may not be efficient for very large strings due to its time complexity of O(n^3), where n is the length of the input string. There are more efficient algorithms for this problem, but this implementation provides a straightforward starting point.

### 1. Algorithms & Data Structures (C++): Valid Anagram

To determine if two strings are valid anagrams of each other in C++, you can use the following approach:

1. Create an array of size 26 to count the occurrences of each letter in the first string.
2. Iterate through the first string and increment the count of each letter in the array.
3. Iterate through the second string and decrement the count of each letter in the array.
4. If at any point during this iteration the count becomes negative or if the counts at the end are not all zero, then the strings are not valid anagrams.
5. If the counts remain zero for all letters after both iterations, then the strings are valid anagrams.

Here's the C++ code for the implementation:

```cpp
#include <iostream>
#include <string>
#include <array>

bool isAnagram(const std::string& s, const std::string& t) {
    if (s.length() != t.length())
        return false;

    std::array<int, 26> count = {0};

    // Count occurrences of characters in the first string
    for (char c : s)
        count[c - 'a']++;

    // Decrement occurrences of characters in the second string
    for (char c : t) {
        count[c - 'a']--;
        if (count[c - 'a'] < 0)
            return false; // If count becomes negative, it's not an anagram
    }

    // Check if all counts are zero
    for (int i : count) {
        if (i != 0)
            return false;
    }

    return true;
}

int main() {
    std::string s1 = "listen";
    std::string s2 = "silent";

    if (isAnagram(s1, s2))
        std::cout << "The strings are anagrams." << std::endl;
    else
        std::cout << "The strings are not anagrams." << std::endl;

    return 0;
}
```

This code compares whether two strings are anagrams of each other. It's case-sensitive and assumes the input strings contain only lowercase alphabetical characters.

### 1. Algorithms & Data Structures (C++): Valid Palindrome

To check if a string is a valid palindrome in C++, you can follow these steps:

1. Remove all non-alphanumeric characters and convert all characters to lowercase to make the comparison case-insensitive.
2. Use two pointers technique to compare characters from the start and end of the string simultaneously.
3. If characters at both pointers are equal, continue comparing until they meet in the middle.
4. If at any point the characters are not equal, return false.
5. If the pointers meet in the middle without any inequality, return true indicating that the string is a valid palindrome.

Here's the C++ code implementing the above steps:

```cpp
#include <iostream>
#include <cctype>

bool isPalindrome(const std::string& s) {
    int left = 0;
    int right = s.length() - 1;

    while (left < right) {
        // Skip non-alphanumeric characters from left
        while (left < right && !isalnum(s[left]))
            left++;
        // Skip non-alphanumeric characters from right
        while (left < right && !isalnum(s[right]))
            right--;

        // Compare characters (case-insensitive)
        if (tolower(s[left]) != tolower(s[right]))
            return false;

        left++;
        right--;
    }
    return true;
}

int main() {
    std::string str;
    std::cout << "Enter a string: ";
    std::getline(std::cin, str);

    if (isPalindrome(str))
        std::cout << "It's a palindrome." << std::endl;
    else
        std::cout << "It's not a palindrome." << std::endl;

    return 0;
}
```

This program takes a string as input, removes non-alphanumeric characters, converts all characters to lowercase, and then checks if the resulting string is a palindrome using the two-pointer technique.

### 1. Algorithms & Data Structures (C++): Valid Paranthesis - Stacks

Sure! Here's a C++ implementation of a function to check if a given string containing only parentheses is valid or not using a stack:

```cpp
#include <iostream>
#include <stack>
#include <string>

bool isValidParentheses(const std::string& s) {
    std::stack<char> st;

    for (char c : s) {
        if (c == '(' || c == '[' || c == '{') {
            st.push(c);
        } else {
            if (st.empty()) return false;
            char top = st.top();
            st.pop();
            if ((c == ')' && top != '(') || (c == ']' && top != '[') || (c == '}' && top != '{')) {
                return false;
            }
        }
    }

    return st.empty();
}

int main() {
    std::string testString = "{[()]}";
    if (isValidParentheses(testString)) {
        std::cout << "Valid parentheses\n";
    } else {
        std::cout << "Invalid parentheses\n";
    }
    return 0;
}
```

This program defines a function `isValidParentheses` that takes a string `s` as input and returns true if the parentheses in the string are valid, and false otherwise. The main logic involves using a stack to keep track of opening parentheses encountered in the string. When a closing parenthesis is encountered, it is checked against the top element of the stack. If they match, the top element is popped from the stack. At the end, if the stack is empty, it means all parentheses matched correctly, and the string is valid.

### 1. Algorithms & Data Structures (C++): Valid Parentheses

Sure, implementing an algorithm to check for valid parentheses in C++ is a common task. Here's a simple implementation using a stack:

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
            char top = stack.top();
            stack.pop();
            if ((c == ')' && top != '(') || 
                (c == ']' && top != '[') || 
                (c == '}' && top != '{')) {
                return false;
            }
        }
    }
    return stack.empty();
}

int main() {
    std::string testString = "{[()]}";
    if (isValid(testString)) {
        std::cout << "The string has valid parentheses." << std::endl;
    } else {
        std::cout << "The string does not have valid parentheses." << std::endl;
    }
    return 0;
}
```

This code uses a stack to keep track of opening parentheses encountered. When a closing parenthesis is encountered, it checks if the stack is empty. If it is, it means there was no corresponding opening parenthesis, so it returns false. If the stack is not empty, it pops the top element and checks if it matches the current closing parenthesis. If it doesn't match, it returns false. Finally, after iterating through the entire string, it checks if the stack is empty. If it is, all parentheses were matched and returns true; otherwise, it returns false.

### 1. Algorithms & Data Structures (C++): Valid Parenthesis

To implement a solution for validating parentheses in a string using C++, you can use a stack data structure. The idea is to iterate through the string, pushing opening parentheses onto the stack and popping them off when a closing parenthesis is encountered. If at any point the stack is empty and we encounter a closing parenthesis or if the closing parenthesis doesn't match the top of the stack, the string is invalid.

Here's a sample C++ code to achieve this:

```cpp
#include <iostream>
#include <stack>
#include <string>

bool isValidParentheses(const std::string& s) {
    std::stack<char> parenStack;

    for (char c : s) {
        if (c == '(' || c == '[' || c == '{') {
            parenStack.push(c);
        } else if (c == ')' || c == ']' || c == '}') {
            if (parenStack.empty()) {
                return false; // Closing parenthesis with no corresponding opening parenthesis
            }
            char top = parenStack.top();
            parenStack.pop();
            if ((c == ')' && top != '(') || (c == ']' && top != '[') || (c == '}' && top != '{')) {
                return false; // Mismatched parenthesis
            }
        }
    }

    return parenStack.empty(); // If the stack is empty, all parentheses are matched
}

int main() {
    std::string testString = "((()))"; // Change this to test different strings
    if (isValidParentheses(testString)) {
        std::cout << "Valid parentheses" << std::endl;
    } else {
        std::cout << "Invalid parentheses" << std::endl;
    }
    return 0;
}
```

This code defines a function `isValidParentheses` which takes a string as input and returns `true` if the parentheses are valid, and `false` otherwise. The `main` function demonstrates how to use this function.

You can modify the `testString` variable in the `main` function to test different strings.

### 1. Algorithms & Data Structures (C++): Validating a String

Validating a string in C++ typically involves checking if the string meets certain criteria or constraints. The criteria can vary depending on the specific requirements of your application. Here's a simple example of validating a string in C++:

```cpp
#include <iostream>
#include <string>
#include <cctype>

bool isValidString(const std::string& str) {
    // Check if the string is empty
    if (str.empty()) {
        std::cout << "String is empty." << std::endl;
        return false;
    }

    // Check if the string contains only alphanumeric characters
    for (char ch : str) {
        if (!std::isalnum(ch)) {
            std::cout << "String contains non-alphanumeric characters." << std::endl;
            return false;
        }
    }

    // Additional validation criteria can be added here...

    return true;
}

int main() {
    std::string input;

    std::cout << "Enter a string: ";
    std::getline(std::cin, input);

    if (isValidString(input)) {
        std::cout << "String is valid." << std::endl;
    } else {
        std::cout << "String is invalid." << std::endl;
    }

    return 0;
}
```

In this example, the `isValidString` function checks if the input string is empty and if it contains only alphanumeric characters using `std::isalnum` function from the `<cctype>` header. You can add more validation criteria according to your requirements, such as checking for specific patterns, lengths, or formats.

Feel free to modify this example according to your specific validation needs.

### 1. Algorithms & Data Structures (C++): Vigenere Cipher

The Vigenère cipher is a method of encrypting alphabetic text by using a simple form of polyalphabetic substitution. It uses a keyword to shift letters in the plaintext, similar to a Caesar cipher but with varying shifts at different positions in the text.

Here's a simple implementation of the Vigenère cipher in C++:

```cpp
#include <iostream>
#include <string>

using namespace std;

string vigenere_encrypt(const string& plaintext, const string& keyword) {
    string ciphertext = "";
    int key_len = keyword.length();

    for (int i = 0; i < plaintext.length(); ++i) {
        char plain_char = plaintext[i];
        char key_char = keyword[i % key_len];
        
        // Convert characters to uppercase
        plain_char = toupper(plain_char);
        key_char = toupper(key_char);

        if (isalpha(plain_char)) {
            // Shift the character by the key
            char encrypted_char = 'A' + ((plain_char - 'A') + (key_char - 'A')) % 26;
            ciphertext += encrypted_char;
        } else {
            // Keep non-alphabetic characters unchanged
            ciphertext += plain_char;
        }
    }

    return ciphertext;
}

string vigenere_decrypt(const string& ciphertext, const string& keyword) {
    string decrypted_text = "";
    int key_len = keyword.length();

    for (int i = 0; i < ciphertext.length(); ++i) {
        char cipher_char = ciphertext[i];
        char key_char = keyword[i % key_len];

        // Convert characters to uppercase
        cipher_char = toupper(cipher_char);
        key_char = toupper(key_char);

        if (isalpha(cipher_char)) {
            // Shift the character back by the key
            char decrypted_char = 'A' + ((cipher_char - 'A') - (key_char - 'A') + 26) % 26;
            decrypted_text += decrypted_char;
        } else {
            // Keep non-alphabetic characters unchanged
            decrypted_text += cipher_char;
        }
    }

    return decrypted_text;
}

int main() {
    string plaintext = "HELLO";
    string keyword = "KEY";

    string encrypted_text = vigenere_encrypt(plaintext, keyword);
    string decrypted_text = vigenere_decrypt(encrypted_text, keyword);

    cout << "Plaintext: " << plaintext << endl;
    cout << "Encrypted: " << encrypted_text << endl;
    cout << "Decrypted: " << decrypted_text << endl;

    return 0;
}
```

This code provides functions for both encryption and decryption of a message using the Vigenère cipher. The `vigenere_encrypt` function takes a plaintext message and a keyword as input and produces the encrypted ciphertext. Similarly, the `vigenere_decrypt` function takes the ciphertext and the keyword and produces the decrypted plaintext.

You can test the code by running it and providing your own plaintext and keyword.

### 1. Algorithms & Data Structures (C++): Vowel Find

Certainly! Here's a simple C++ function to find and count vowels in a given string using basic algorithms and data structures:

```cpp
#include <iostream>
#include <string>
#include <unordered_set>

int countVowels(const std::string& str) {
    // Set up a set of vowels for efficient lookup
    std::unordered_set<char> vowels = {'a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'};
    
    int count = 0;
    // Iterate through each character in the string
    for (char c : str) {
        // Check if the character is a vowel
        if (vowels.count(c) > 0) {
            count++;
        }
    }
    return count;
}

int main() {
    std::string input;
    std::cout << "Enter a string: ";
    std::getline(std::cin, input);
    
    int vowelCount = countVowels(input);
    std::cout << "Number of vowels: " << vowelCount << std::endl;
    
    return 0;
}
```

This code defines a function `countVowels` that takes a string and returns the count of vowels in it. It iterates through each character of the string and checks if it's a vowel using a set for efficient lookup. The main function prompts the user to input a string, calls `countVowels`, and prints the count of vowels found.

### 1. Algorithms & Data Structures (C++): Word ladder

A word ladder is a classic problem in computer science and involves transforming one word into another by changing one letter at a time, with each intermediate step forming a valid word. Here's an outline of how you might implement a word ladder algorithm in C++ using breadth-first search (BFS) and a suitable data structure, such as a queue.

```cpp
#include <iostream>
#include <unordered_set>
#include <queue>
#include <unordered_map>
#include <vector>
#include <string>

using namespace std;

// Function to find the shortest transformation sequence from start to end
vector<string> findLadder(string start, string end, unordered_set<string>& wordList) {
    vector<string> ladder;
    if (start == end)
        return ladder;

    // Queue for BFS
    queue<string> q;
    q.push(start);

    // Map to store the parent of each word in the ladder
    unordered_map<string, string> parent;
    parent[start] = "";

    while (!q.empty()) {
        int size = q.size();
        unordered_set<string> levelVisited;

        for (int i = 0; i < size; ++i) {
            string curr = q.front();
            q.pop();

            // Generate all possible words by changing one character at a time
            for (int j = 0; j < curr.size(); ++j) {
                string temp = curr;
                for (char c = 'a'; c <= 'z'; ++c) {
                    temp[j] = c;
                    if (temp == end) {
                        // Found the end word, reconstruct ladder
                        string word = end;
                        ladder.push_back(word);
                        while (parent[word] != "") {
                            ladder.push_back(parent[word]);
                            word = parent[word];
                        }
                        reverse(ladder.begin(), ladder.end());
                        return ladder;
                    }
                    if (wordList.count(temp) && !parent.count(temp)) {
                        q.push(temp);
                        levelVisited.insert(temp);
                        parent[temp] = curr;
                    }
                }
            }
        }
        // Remove words from wordList to avoid revisiting in subsequent levels
        for (const auto& word : levelVisited) {
            wordList.erase(word);
        }
    }

    return ladder; // No ladder found
}

int main() {
    string start = "hit";
    string end = "cog";
    unordered_set<string> wordList = {"hot", "dot", "dog", "lot", "log"};

    vector<string> ladder = findLadder(start, end, wordList);

    if (ladder.empty()) {
        cout << "No ladder found!" << endl;
    } else {
        cout << "Shortest ladder from " << start << " to " << end << ":" << endl;
        for (const auto& word : ladder) {
            cout << word << " ";
        }
        cout << endl;
    }

    return 0;
}
```

In this implementation, we use a BFS approach to explore all possible transformations from the start word. We keep track of the parent of each word to reconstruct the ladder once we find the end word. We also maintain a set to mark visited words in each level to avoid revisiting them.

### 1. Algorithms & Data Structures (C++): Word ladder: Complexity analysis

For a word ladder problem, where you have to transform one word into another by changing one letter at a time, complexity analysis involves considering both time and space complexities. Let's break it down:

1. **Time Complexity**:

   - **Building Graph**: Constructing the graph where each node represents a word and each edge represents a connection between words that differ by one letter, takes O(n * m^2) time, where n is the number of words and m is the length of each word. For each word, we need to compare it with every other word, which takes O(m) time, and for each comparison, we need to check if they differ by just one letter, which also takes O(m) time.

   - **Breadth-First Search (BFS)**: Performing a BFS to find the shortest transformation sequence from the start word to the end word takes O(V + E) time, where V is the number of vertices (words) and E is the number of edges (connections between words). In the worst-case scenario, where every word can be transformed into every other word, both V and E can be as large as O(n^2).

   - **Total Time Complexity**: O(n * m^2 + n^2)

2. **Space Complexity**:

   - **Graph**: The graph representation typically requires O(n * m^2) space, as each word (node) is associated with a list of adjacent words (edges).

   - **Visited Set**: During BFS, we need to keep track of visited nodes to avoid revisiting them. This requires additional space of O(n).

   - **Queue**: The BFS queue can hold at most O(n) words.

   - **Total Space Complexity**: O(n * m^2)

In summary, the time complexity of the word ladder problem is dominated by constructing the graph, while the space complexity is primarily determined by the graph representation. It's worth noting that the actual performance may vary based on the implementation details and the specific characteristics of the input words.

### 1. Algorithms & Data Structures (C++): Word search

A word search algorithm in C++ typically involves searching for words within a grid of letters, checking horizontally, vertically, and diagonally. Here's a simple implementation:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

bool isValid(int x, int y, int rows, int cols) {
    return x >= 0 && x < rows && y >= 0 && y < cols;
}

bool searchWord(vector<vector<char>>& grid, string word, int x, int y, int dx, int dy) {
    int len = word.length();
    int rows = grid.size();
    int cols = grid[0].size();

    for (int i = 0; i < len; ++i) {
        if (!isValid(x, y, rows, cols) || grid[x][y] != word[i])
            return false;
        x += dx;
        y += dy;
    }
    return true;
}

bool wordSearch(vector<vector<char>>& grid, string word) {
    int rows = grid.size();
    int cols = grid[0].size();

    // Directions: horizontal, vertical, diagonal (left-up to right-down), diagonal (right-up to left-down)
    int dx[] = {0, 1, 1, 1};
    int dy[] = {1, 0, 1, -1};

    for (int i = 0; i < rows; ++i) {
        for (int j = 0; j < cols; ++j) {
            for (int k = 0; k < 4; ++k) {
                if (searchWord(grid, word, i, j, dx[k], dy[k]))
                    return true;
            }
        }
    }
    return false;
}

int main() {
    vector<vector<char>> grid = {
        {'A', 'B', 'C', 'E'},
        {'S', 'F', 'C', 'S'},
        {'A', 'D', 'E', 'E'}
    };

    string word = "ABCCED";
    if (wordSearch(grid, word))
        cout << "Word found!" << endl;
    else
        cout << "Word not found." << endl;

    return 0;
}
```

In this implementation:

- `isValid()` function checks if a given position `(x, y)` is within the bounds of the grid.
- `searchWord()` function checks if the given word exists starting from position `(x, y)` with a given direction `(dx, dy)`.
- `wordSearch()` function iterates through each cell of the grid and for each cell, it tries to search for the word in all four directions (horizontal, vertical, and both diagonals).
- In the `main()` function, a sample grid and word are provided, and the `wordSearch()` function is called to check if the word exists in the grid.

You can modify the `main()` function to test with different words and grids.

### 1. Algorithms & Data Structures (C++): Word search: Complexity analysis

In a word search problem, the typical approach is to search for a given word within a grid of letters, where the word can be found horizontally, vertically, or diagonally. Here's a brief complexity analysis for a common algorithm used to solve this problem:

#### Brute Force Approach

**Algorithm:**

1. Iterate through each cell in the grid.
2. For each cell, start a search to find the word horizontally, vertically, and diagonally.
3. If the word is found, return true; otherwise, continue searching.
4. If the entire grid is traversed and the word is not found, return false.

**Complexity:**

- Let \( n \) be the number of rows and \( m \) be the number of columns in the grid.
- Let \( k \) be the length of the word we are searching for.

1. **Time Complexity:**
   - In the worst case, for each cell in the grid, we perform up to 8 searches (horizontally, vertically, and diagonally).
   - So, the time complexity is approximately \( O(n \times m \times 8 \times k) \).
   - Simplifying, this is \( O(n \times m \times k) \).

2. **Space Complexity:**
   - We don't use any extra space that grows with the input size, so the space complexity is constant, \( O(1) \).

#### Optimized Approach (Trie + Backtracking)

**Algorithm:**

1. Build a trie data structure containing all the words to be searched.
2. Iterate through each cell in the grid.
3. For each cell, perform a backtracking search using the trie to check for valid words.
4. If a valid word is found, mark it as visited and continue the search.
5. If the search reaches a dead-end or exhausts all possibilities, backtrack and try another path.

**Complexity:**

- Let \( n \) be the number of rows and \( m \) be the number of columns in the grid.
- Let \( k \) be the length of the longest word to be searched.
- Let \( l \) be the total number of characters in all the words.

1. **Time Complexity:**
   - Building the trie takes \( O(l) \) time.
   - Each cell of the grid can be visited at most once in a single path of the backtracking search.
   - In the worst case, the backtracking search might explore all possible paths for each starting cell, which results in \( O(n \times m \times 8^k) \).
   - Overall time complexity is \( O(l + n \times m \times 8^k) \).

2. **Space Complexity:**
   - The space complexity is dominated by the trie structure, which takes \( O(l) \) space.
   - Additionally, in the backtracking algorithm, we use recursion, which consumes stack space proportional to the maximum depth of recursion, which can be up to \( O(k) \).
   - So, the total space complexity is \( O(l + k) \).

The optimized approach has a better time complexity compared to the brute force approach, especially for large grids or a large number of words. However, the space complexity increases due to the trie data structure.

### 1. Algorithms & Data Structures (C++): Word Subsets

In C++, implementing a solution for word subsets involves a few steps. First, you need to find the count of each letter in each word of the second list (the "subsets"). Then, you need to compare these counts with those of the first list (the "words"). If all the counts in the subset are greater than or equal to their corresponding counts in the word, then the word is considered a subset of the given word.

Here's a basic implementation using a frequency array to count the occurrences of each letter:

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>

using namespace std;

vector<int> countLetters(const string& word) {
    vector<int> counts(26, 0); // Assuming lowercase English letters only
    for (char ch : word) {
        counts[ch - 'a']++;
    }
    return counts;
}

vector<int> mergeCounts(const vector<int>& counts1, const vector<int>& counts2) {
    vector<int> mergedCounts(26, 0);
    for (int i = 0; i < 26; ++i) {
        mergedCounts[i] = max(counts1[i], counts2[i]);
    }
    return mergedCounts;
}

bool isSubset(const string& word, const vector<int>& subsetCounts) {
    vector<int> wordCounts = countLetters(word);
    for (int i = 0; i < 26; ++i) {
        if (subsetCounts[i] > wordCounts[i]) {
            return false;
        }
    }
    return true;
}

vector<string> wordSubsets(const vector<string>& words, const vector<string>& subsets) {
    vector<int> globalCounts(26, 0);
    for (const string& subset : subsets) {
        vector<int> subsetCounts = countLetters(subset);
        globalCounts = mergeCounts(globalCounts, subsetCounts);
    }

    vector<string> result;
    for (const string& word : words) {
        if (isSubset(word, globalCounts)) {
            result.push_back(word);
        }
    }
    return result;
}

int main() {
    vector<string> words = {"amazon", "apple", "facebook", "google", "leetcode"};
    vector<string> subsets = {"e", "o"};
    vector<string> result = wordSubsets(words, subsets);
    cout << "Word Subsets: ";
    for (const string& word : result) {
        cout << word << " ";
    }
    cout << endl;
    return 0;
}
```

This code first calculates the global counts of each letter in the subsets. Then, it checks each word to see if it is a subset by comparing its letter counts with the global counts. Finally, it returns the subset words.

### 1. Algorithms & Data Structures (C++): ZigZag Conversion

Zigzag conversion is a common string manipulation problem where you're asked to convert a string in a zigzag pattern given a certain number of rows. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <string>
#include <vector>

std::string convert(std::string s, int numRows) {
    if (numRows == 1) return s; // If there's only one row, return the string as it is

    std::vector<std::string> rows(std::min(numRows, int(s.size()))); // Vector of strings to hold rows
    int currentRow = 0;
    bool goingDown = false;

    for (char c : s) {
        rows[currentRow] += c; // Append current character to the current row
        if (currentRow == 0 || currentRow == numRows - 1) // If we're at the first or last row
            goingDown = !goingDown; // Change direction
        currentRow += goingDown ? 1 : -1; // Move to the next or previous row based on direction
    }

    std::string result;
    for (const std::string& row : rows) {
        result += row; // Concatenate all rows to get the final result
    }
    return result;
}

int main() {
    std::string s = "PAYPALISHIRING";
    int numRows = 3;
    std::cout << "Original string: " << s << std::endl;
    std::cout << "Zigzag converted string: " << convert(s, numRows) << std::endl;
    return 0;
}
```

This code defines a function `convert` that takes a string `s` and the number of rows `numRows` and returns the zigzag converted string. The main logic is to iterate through the input string `s`, appending characters to the appropriate row, and then concatenating all the rows to get the final result.

For example, if `s` is "PAYPALISHIRING" and `numRows` is 3, the zigzag converted string would be "PAHNAPLSIIGYIR". You can adjust `numRows` to change the pattern.

### 1. Algorithms & Data Structures (C++): Subsequences

Subsequences in computer science, particularly in the context of algorithms and data structures, refer to a sequence that can be derived from another sequence by deleting some or no elements without changing the order of the remaining elements.

In C++, you can find subsequences using recursion or dynamic programming, depending on the problem's complexity. Here's a simple example of finding all subsequences of a given string using recursion:

```cpp
#include <iostream>
#include <string>
using namespace std;

void findSubsequences(string str, string subsequence, int index) {
    // Print current subsequence
    cout << subsequence << endl;

    for (int i = index; i < str.length(); ++i) {
        // Include current character
        subsequence += str[i];

        // Exclude current character and consider next character
        findSubsequences(str, subsequence, i + 1);

        // Backtrack
        subsequence.pop_back();
    }
}

int main() {
    string str = "abc";
    findSubsequences(str, "", 0);
    return 0;
}
```

This code will output all possible subsequences of the string "abc":

```bash
a
ab
abc
ac
b
bc
c
```

For more complex problems involving subsequences, such as finding the longest common subsequence between two strings or the maximum sum subsequence in an array, dynamic programming is often used for efficiency.
