
### 1. Algorithms & Data Structures (C++): Common Operations on Trie (Creation)

In C++, implementing common operations on a trie involves creating, searching, inserting, and deleting nodes efficiently. Let's start with creating a trie:

```cpp
#include <iostream>
#include <unordered_map>

using namespace std;

// Trie Node
struct TrieNode {
    unordered_map<char, TrieNode*> children;
    bool isEndOfWord;

    TrieNode() {
        isEndOfWord = false;
    }
};

// Trie class
class Trie {
private:
    TrieNode* root;

public:
    Trie() {
        root = new TrieNode();
    }

    // Function to insert a word into the trie
    void insert(string word) {
        TrieNode* current = root;
        for (char ch : word) {
            if (current->children.find(ch) == current->children.end()) {
                current->children[ch] = new TrieNode();
            }
            current = current->children[ch];
        }
        current->isEndOfWord = true; // Mark end of word
    }

    // Function to search for a word in the trie
    bool search(string word) {
        TrieNode* current = root;
        for (char ch : word) {
            if (current->children.find(ch) == current->children.end()) {
                return false; // Character not found
            }
            current = current->children[ch];
        }
        return current->isEndOfWord; // Return true if end of word reached
    }
};

int main() {
    Trie trie;
    trie.insert("hello");
    trie.insert("world");

    cout << boolalpha;
    cout << trie.search("hello") << endl; // Output: true
    cout << trie.search("world") << endl; // Output: true
    cout << trie.search("hell") << endl;  // Output: false

    return 0;
}
```

This code demonstrates the creation of a trie and insertion of words into it. The `TrieNode` struct represents each node in the trie, containing a map of children nodes and a boolean flag indicating if it's the end of a word. The `Trie` class encapsulates the trie data structure and provides methods like `insert` and `search` for common operations.

### 1. Algorithms & Data Structures (C++): Data Structure: Trie

A Trie, also known as a prefix tree, is a tree-like data structure that is used to store a dynamic set of strings where the keys are usually strings. Each node in a Trie represents a common prefix of a set of strings. It is particularly useful for tasks like autocomplete features in text editors, spell checkers, and IP routing tables.

In C++, you can implement a Trie using classes and pointers. Here's a basic implementation to get you started:

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
    TrieNode* root;

public:
    Trie() {
        root = new TrieNode();
    }

    void insert(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                current->children[c] = new TrieNode();
            }
            current = current->children[c];
        }
        current->isEndOfWord = true;
    }

    bool search(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                return false;
            }
            current = current->children[c];
        }
        return current->isEndOfWord;
    }

    bool startsWith(string prefix) {
        TrieNode* current = root;
        for (char c : prefix) {
            if (current->children.find(c) == current->children.end()) {
                return false;
            }
            current = current->children[c];
        }
        return true;
    }
};

int main() {
    Trie trie;
    trie.insert("apple");
    cout << trie.search("apple") << endl;   // Output: 1 (true)
    cout << trie.search("app") << endl;     // Output: 0 (false)
    cout << trie.startsWith("app") << endl; // Output: 1 (true)
    trie.insert("app");
    cout << trie.search("app") << endl;     // Output: 1 (true)
    return 0;
}
```

In this implementation, each node of the Trie is represented by the `TrieNode` class. The `Trie` class maintains the root of the Trie and provides methods for inserting, searching, and checking if a word starts with a given prefix.

### 1. Algorithms & Data Structures (C++): Delete a string from Trie

Deleting a string from a Trie (also known as a Prefix Tree) involves a few steps. Here's a basic outline of how you can achieve this in C++:

```cpp
#include <iostream>
#include <unordered_map>

using namespace std;

// Trie Node
struct TrieNode {
    unordered_map<char, TrieNode*> children;
    bool isEndOfWord;
    
    TrieNode() {
        isEndOfWord = false;
    }
};

// Trie class
class Trie {
private:
    TrieNode* root;
    
public:
    Trie() {
        root = new TrieNode();
    }
    
    // Insert a word into the Trie
    void insert(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                current->children[c] = new TrieNode();
            }
            current = current->children[c];
        }
        current->isEndOfWord = true;
    }
    
    // Search if a word exists in the Trie
    bool search(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                return false;
            }
            current = current->children[c];
        }
        return current != nullptr && current->isEndOfWord;
    }
    
    // Helper function to check if a node has no children
    bool hasNoChildren(TrieNode* node) {
        for (auto& pair : node->children) {
            if (pair.second != nullptr) {
                return false;
            }
        }
        return true;
    }
    
    // Delete a word from the Trie
    bool deleteWord(string word) {
        return deleteHelper(root, word, 0);
    }
    
    // Recursive helper function to delete a word from the Trie
    bool deleteHelper(TrieNode* current, string word, int index) {
        if (index == word.length()) {
            if (!current->isEndOfWord) {
                return false; // Word not found
            }
            current->isEndOfWord = false;
            return hasNoChildren(current); // Check if current node can be deleted
        }
        
        char ch = word[index];
        if (current->children.find(ch) == current->children.end()) {
            return false; // Word not found
        }
        
        bool shouldDeleteCurrentNode = deleteHelper(current->children[ch], word, index + 1);
        
        // Delete the child node if necessary
        if (shouldDeleteCurrentNode) {
            current->children[ch] = nullptr;
            delete current->children[ch];
            return hasNoChildren(current) && !current->isEndOfWord;
        }
        
        return false;
    }
};

int main() {
    Trie trie;
    trie.insert("apple");
    trie.insert("app");
    trie.insert("banana");
    
    cout << "Before deletion:\n";
    cout << "Is 'apple' present? " << (trie.search("apple") ? "Yes" : "No") << endl;
    cout << "Is 'app' present? " << (trie.search("app") ? "Yes" : "No") << endl;
    cout << "Is 'banana' present? " << (trie.search("banana") ? "Yes" : "No") << endl;
    
    trie.deleteWord("app");
    
    cout << "\nAfter deletion of 'app':\n";
    cout << "Is 'apple' present? " << (trie.search("apple") ? "Yes" : "No") << endl;
    cout << "Is 'app' present? " << (trie.search("app") ? "Yes" : "No") << endl;
    cout << "Is 'banana' present? " << (trie.search("banana") ? "Yes" : "No") << endl;
    
    return 0;
}
```

In this code:

1. We define a TrieNode structure which holds a map of characters to TrieNode pointers representing the children of the current node, and a boolean flag indicating if it's the end of a word.
2. We implement the Trie class with methods for insertion, search, and deletion of words.
3. The `deleteWord` method first finds the word to be deleted using a recursive helper function `deleteHelper`. It then removes the end of word marker and recursively deletes nodes until it reaches a point where it can delete the current node safely.
4. The `hasNoChildren` function checks if a node has no children, indicating that it can be safely deleted.
5. In the main function, we demonstrate the usage of the Trie class by inserting some words, searching for them, and then deleting one of them.

### 1. Algorithms & Data Structures (C++): Insert a string in Trie

Sure! Below is a C++ implementation of inserting a string into a Trie data structure:

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
    
    void insert(string word) {
        TrieNode* curr = root;
        for (char c : word) {
            if (curr->children.find(c) == curr->children.end()) {
                curr->children[c] = new TrieNode();
            }
            curr = curr->children[c];
        }
        curr->isEndOfWord = true;
    }
    
    bool search(string word) {
        TrieNode* curr = root;
        for (char c : word) {
            if (curr->children.find(c) == curr->children.end()) {
                return false;
            }
            curr = curr->children[c];
        }
        return curr->isEndOfWord;
    }
};

int main() {
    Trie trie;
    trie.insert("apple");
    trie.insert("banana");
    trie.insert("orange");
    
    cout << "Search 'apple': " << (trie.search("apple") ? "Found" : "Not found") << endl;
    cout << "Search 'orange': " << (trie.search("orange") ? "Found" : "Not found") << endl;
    cout << "Search 'grape': " << (trie.search("grape") ? "Found" : "Not found") << endl;
    
    return 0;
}
```

This code defines a Trie data structure with methods for insertion and searching. The `TrieNode` class represents each node in the Trie, containing a map of child nodes and a boolean flag to indicate if it's the end of a word. The `Trie` class provides methods to insert a word into the Trie and search for a word within it. In the `main` function, we demonstrate inserting some words into the Trie and searching for them.

### 1. Algorithms & Data Structures (C++): Insert in Trie

Sure, here's a basic implementation of inserting a word into a Trie (also known as a Prefix Tree) in C++:

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

    bool search(const string& word) {
        TrieNode* current = root;
        for (char ch : word) {
            if (current->children.find(ch) == current->children.end()) {
                return false;
            }
            current = current->children[ch];
        }
        return current->isEndOfWord;
    }
};

int main() {
    Trie trie;
    trie.insert("hello");
    trie.insert("world");

    cout << "Searching for 'hello': " << (trie.search("hello") ? "Found" : "Not Found") << endl;
    cout << "Searching for 'world': " << (trie.search("world") ? "Found" : "Not Found") << endl;
    cout << "Searching for 'hey': " << (trie.search("hey") ? "Found" : "Not Found") << endl;

    return 0;
}
```

This code defines two classes: `TrieNode`, which represents a single node in the Trie, and `Trie`, which is the Trie data structure itself. The `insert` function inserts a word into the Trie, and the `search` function checks if a given word exists in the Trie.

Each node in the Trie has an unordered map to store its children, representing the characters that can follow the current node. The `isEndOfWord` flag is set to true for nodes that represent the end of a word.

### 1. Algorithms & Data Structures (C++): Maximum XOR Pair

To find the maximum XOR pair in an array of integers, you can use a Trie data structure. Here's a step-by-step approach to implement it in C++:

1. Define a TrieNode structure to represent each node in the Trie.
2. Implement Trie insertion and search functions.
3. Traverse the array of integers and insert their binary representations into the Trie.
4. For each integer, find its XOR complement by traversing the Trie.
5. Track the maximum XOR value found during traversal.

Here's a sample implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Trie Node
struct TrieNode {
    TrieNode* children[2]; // Represents 0 and 1
    TrieNode() {
        children[0] = nullptr;
        children[1] = nullptr;
    }
};

// Trie Class
class Trie {
public:
    Trie() {
        root = new TrieNode();
    }

    // Insert a number into the Trie
    void insert(int num) {
        TrieNode* curr = root;
        for (int i = 31; i >= 0; --i) {
            int bit = (num >> i) & 1;
            if (!curr->children[bit])
                curr->children[bit] = new TrieNode();
            curr = curr->children[bit];
        }
    }

    // Find maximum XOR of a number with all numbers in the Trie
    int findMaxXOR(int num) {
        TrieNode* curr = root;
        int maxXOR = 0;
        for (int i = 31; i >= 0; --i) {
            int bit = (num >> i) & 1;
            int complement = 1 - bit; // XOR complement
            if (curr->children[complement]) {
                maxXOR |= (1 << i);
                curr = curr->children[complement];
            } else {
                curr = curr->children[bit];
            }
        }
        return maxXOR;
    }

private:
    TrieNode* root;
};

// Function to find maximum XOR pair in an array
int findMaximumXOR(const vector<int>& nums) {
    Trie trie;
    int maxXOR = 0;
    for (int num : nums) {
        trie.insert(num);
        maxXOR = max(maxXOR, trie.findMaxXOR(num));
    }
    return maxXOR;
}

int main() {
    vector<int> nums = {3, 10, 5, 25, 2, 8};
    cout << "Maximum XOR pair: " << findMaximumXOR(nums) << endl;
    return 0;
}
```

This code initializes a Trie data structure, inserts each number's binary representation into the Trie, and then finds the maximum XOR pair by traversing the Trie for each number. Finally, it outputs the maximum XOR value found.

### 1. Algorithms & Data Structures (C++): Maximum Xor Queries

To implement Maximum XOR Queries efficiently, you can use a Trie data structure. Here's a step-by-step approach to implementing this algorithm in C++:

1. Define the TrieNode structure to represent each node in the Trie.
2. Implement the insert function to insert a number into the Trie.
3. Implement the maxXOR function to find the maximum XOR value for a given number.

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Trie Node
struct TrieNode {
    TrieNode* children[2]; // Two children: 0 and 1
    TrieNode() {
        children[0] = nullptr;
        children[1] = nullptr;
    }
};

// Trie class
class Trie {
public:
    TrieNode* root;

    Trie() {
        root = new TrieNode();
    }

    // Insert a number into the trie
    void insert(int num) {
        TrieNode* curr = root;
        for (int i = 31; i >= 0; i--) {
            int bit = (num >> i) & 1;
            if (curr->children[bit] == nullptr)
                curr->children[bit] = new TrieNode();
            curr = curr->children[bit];
        }
    }

    // Find the maximum XOR value for a given number
    int maxXOR(int num) {
        TrieNode* curr = root;
        int result = 0;
        for (int i = 31; i >= 0; i--) {
            int bit = (num >> i) & 1;
            int complement = 1 - bit;
            if (curr->children[complement] != nullptr) {
                result |= (1 << i); // Set the ith bit of result to 1
                curr = curr->children[complement];
            } else {
                curr = curr->children[bit];
            }
        }
        return result;
    }
};

// Function to find maximum XOR values for each query
vector<int> maxXorQueries(const vector<int>& nums, const vector<pair<int, int>>& queries) {
    Trie trie;
    for (int num : nums) {
        trie.insert(num);
    }

    vector<int> results;
    for (auto& query : queries) {
        int result = trie.maxXOR(query.first);
        results.push_back(result ^ query.first); // XOR the result with the query number itself
    }
    return results;
}

int main() {
    vector<int> nums = {3, 10, 5, 25, 2, 8};
    vector<pair<int, int>> queries = {{0, 1}, {1, 2}, {2, 3}, {3, 4}, {4, 5}};
    vector<int> results = maxXorQueries(nums, queries);
    for (int result : results) {
        cout << result << " ";
    }
    return 0;
}
```

This implementation efficiently finds the maximum XOR value for each query using the Trie data structure.

### 1. Algorithms & Data Structures (C++): Practical use of Trie

Tries, or prefix trees, are versatile data structures commonly used in string-related problems. Here are several practical use cases for tries in C++:

1. **Auto-Complete or Spell Check**: Tries are excellent for implementing auto-complete or spell-check functionalities. As you type a word, the trie can quickly find all valid completions or suggest corrections based on the stored dictionary of words.

2. **Dictionary Implementations**: Tries are often used to implement dictionaries or sets of strings efficiently. Each node in the trie represents a character, and by traversing the trie, you can insert, search, or delete words in logarithmic time complexity relative to the length of the word.

3. **Routing Tables in Computer Networks**: Tries can be used to implement routing tables in computer networks. Each node in the trie represents a part of the IP address, and by traversing the trie, routers can efficiently determine the next hop for a given IP address.

4. **Finding Longest Common Prefix**: Tries are useful for finding the longest common prefix among a set of strings. By traversing the trie, you can identify the deepest common node shared among the strings.

5. **IP Address Lookup**: Tries can be used to perform IP address lookups efficiently. Each node in the trie represents a part of the IP address, and by traversing the trie, you can determine the corresponding information associated with that IP address.

6. **Implementing Contact Lists or Phone Books**: Tries can be used to implement contact lists or phone books efficiently. Each node represents a character in a contact's name, and by traversing the trie, you can quickly search for contacts or perform operations like adding or deleting contacts.

In C++, you can implement a trie using a class structure where each node contains an array or a map of pointers to its child nodes, representing characters. Here's a basic outline of how you could implement a trie in C++:

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

    void insert(string word) {
        TrieNode* current = root;
        for (char ch : word) {
            if (current->children.find(ch) == current->children.end()) {
                current->children[ch] = new TrieNode();
            }
            current = current->children[ch];
        }
        current->isEndOfWord = true;
    }

    bool search(string word) {
        TrieNode* current = root;
        for (char ch : word) {
            if (current->children.find(ch) == current->children.end()) {
                return false;
            }
            current = current->children[ch];
        }
        return current != nullptr && current->isEndOfWord;
    }

    bool startsWith(string prefix) {
        TrieNode* current = root;
        for (char ch : prefix) {
            if (current->children.find(ch) == current->children.end()) {
                return false;
            }
            current = current->children[ch];
        }
        return current != nullptr;
    }
};

int main() {
    Trie trie;
    trie.insert("apple");
    cout << trie.search("apple") << endl;   // Output: 1 (true)
    cout << trie.search("app") << endl;     // Output: 0 (false)
    cout << trie.startsWith("app") << endl; // Output: 1 (true)
    trie.insert("app");
    cout << trie.search("app") << endl;     // Output: 1 (true)
    return 0;
}
```

This implementation provides basic functionalities like insertion, search, and prefix search. You can extend it to suit your specific use case.

### 1. Algorithms & Data Structures (C++): Prefix Trie Data Structure Solution

Sure! Here's a simple implementation of a Prefix Trie data structure in C++:

```cpp
#include <iostream>
#include <unordered_map>
#include <string>

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

    void insert(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                current->children[c] = new TrieNode();
            }
            current = current->children[c];
        }
        current->isEndOfWord = true;
    }

    bool search(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                return false;
            }
            current = current->children[c];
        }
        return current->isEndOfWord;
    }

    bool startsWith(string prefix) {
        TrieNode* current = root;
        for (char c : prefix) {
            if (current->children.find(c) == current->children.end()) {
                return false;
            }
            current = current->children[c];
        }
        return true;
    }
};

int main() {
    Trie trie;

    trie.insert("apple");
    cout << "Search 'apple': " << (trie.search("apple") ? "Found" : "Not Found") << endl;
    cout << "Search 'app': " << (trie.search("app") ? "Found" : "Not Found") << endl;
    cout << "Starts with 'app': " << (trie.startsWith("app") ? "True" : "False") << endl;

    return 0;
}
```

This code defines two classes: `TrieNode` and `Trie`. `TrieNode` represents a node in the Trie, and `Trie` is the actual Trie data structure.

The `insert` function inserts a word into the Trie, `search` checks if a word exists in the Trie, and `startsWith` checks if there are any words in the Trie that start with a given prefix.

You can use this code as a foundation for more complex Trie operations or extend it to suit your specific needs.

### 1. Algorithms & Data Structures (C++): Search for a string in Trie

Certainly! Implementing a Trie (prefix tree) in C++ to search for a string involves creating a data structure that efficiently stores a set of strings and supports fast searching operations. Here's a basic implementation of a Trie along with a function to search for a string within it:

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
public:
    TrieNode* root;

    Trie() {
        root = new TrieNode();
    }

    void insert(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                current->children[c] = new TrieNode();
            }
            current = current->children[c];
        }
        current->isEndOfWord = true;
    }

    bool search(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                return false; // Character not found, word not present
            }
            current = current->children[c];
        }
        return current->isEndOfWord; // Return true only if it's the end of a word
    }
};

int main() {
    Trie trie;
    trie.insert("hello");
    trie.insert("world");
    trie.insert("hey");
    trie.insert("hi");

    cout << "Search for 'hello': " << (trie.search("hello") ? "Found" : "Not found") << endl;
    cout << "Search for 'world': " << (trie.search("world") ? "Found" : "Not found") << endl;
    cout << "Search for 'hey': " << (trie.search("hey") ? "Found" : "Not found") << endl;
    cout << "Search for 'hi': " << (trie.search("hi") ? "Found" : "Not found") << endl;
    cout << "Search for 'openai': " << (trie.search("openai") ? "Found" : "Not found") << endl;

    return 0;
}
```

In this code:

- `TrieNode` represents each node in the Trie, containing a map of child nodes and a boolean indicating whether it's the end of a word.
- `Trie` is the Trie data structure with methods to insert and search strings.
- `insert` method inserts a word into the Trie.
- `search` method searches for a word in the Trie.

You can extend this implementation further by adding methods for deleting strings, finding all words with a given prefix, and other functionalities as needed.

### 1. Algorithms & Data Structures (C++): Search in Trie

Searching in a Trie (also known as prefix tree) is a fundamental operation in computer science. It's commonly used in tasks like autocomplete, spell checking, and searching for words with a given prefix. Here's how you can implement search in a Trie using C++:

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

    void insert(string word) {
        TrieNode* curr = root;
        for (char c : word) {
            if (curr->children.find(c) == curr->children.end()) {
                curr->children[c] = new TrieNode();
            }
            curr = curr->children[c];
        }
        curr->isEndOfWord = true;
    }

    bool search(string word) {
        TrieNode* curr = root;
        for (char c : word) {
            if (curr->children.find(c) == curr->children.end()) {
                return false; // character not found
            }
            curr = curr->children[c];
        }
        return curr->isEndOfWord; // return true if end of word is reached
    }
};

int main() {
    Trie trie;
    trie.insert("apple");
    trie.insert("banana");
    trie.insert("orange");

    cout << "Searching for 'apple': " << (trie.search("apple") ? "Found" : "Not Found") << endl;
    cout << "Searching for 'banana': " << (trie.search("banana") ? "Found" : "Not Found") << endl;
    cout << "Searching for 'orange': " << (trie.search("orange") ? "Found" : "Not Found") << endl;
    cout << "Searching for 'grape': " << (trie.search("grape") ? "Found" : "Not Found") << endl;

    return 0;
}
```

This code demonstrates a basic Trie implementation in C++. The `TrieNode` class represents a single node in the Trie, while the `Trie` class provides methods to insert words into the Trie and search for words in the Trie. The `search` method checks if a given word exists in the Trie by traversing down the Trie from the root, character by character. If at any point a character is not found or the end of the word is reached and `isEndOfWord` is false, the search returns false. Otherwise, it returns true.

### 1. Algorithms & Data Structures (C++): Suffix Trie

A Suffix Trie is a data structure used for efficient string matching and searching. It's particularly useful for tasks such as finding all occurrences of a pattern in a text or checking if a string contains a particular substring. Here's a basic implementation of a suffix trie in C++:

```cpp
#include <iostream>
#include <unordered_map>
#include <string>

using namespace std;

class SuffixTrieNode {
public:
    unordered_map<char, SuffixTrieNode*> children;
    bool isEndOfWord;

    SuffixTrieNode() {
        isEndOfWord = false;
    }
};

class SuffixTrie {
public:
    SuffixTrieNode* root;

    SuffixTrie() {
        root = new SuffixTrieNode();
    }

    void insert(string word) {
        SuffixTrieNode* current = root;
        for (int i = 0; i < word.length(); i++) {
            char ch = word[i];
            if (current->children.find(ch) == current->children.end()) {
                current->children[ch] = new SuffixTrieNode();
            }
            current = current->children[ch];
        }
        current->isEndOfWord = true;
    }

    bool search(string word) {
        SuffixTrieNode* current = root;
        for (int i = 0; i < word.length(); i++) {
            char ch = word[i];
            if (current->children.find(ch) == current->children.end()) {
                return false;
            }
            current = current->children[ch];
        }
        return current != nullptr && current->isEndOfWord;
    }
};

int main() {
    SuffixTrie trie;
    trie.insert("hello");
    trie.insert("world");
    trie.insert("hell");
    trie.insert("hi");
    
    cout << "Searching for 'hello': " << (trie.search("hello") ? "Found" : "Not found") << endl;
    cout << "Searching for 'world': " << (trie.search("world") ? "Found" : "Not found") << endl;
    cout << "Searching for 'hell': " << (trie.search("hell") ? "Found" : "Not found") << endl;
    cout << "Searching for 'hi': " << (trie.search("hi") ? "Found" : "Not found") << endl;
    cout << "Searching for 'he': " << (trie.search("he") ? "Found" : "Not found") << endl;
    cout << "Searching for 'cat': " << (trie.search("cat") ? "Found" : "Not found") << endl;
    
    return 0;
}
```

In this implementation:

- `SuffixTrieNode` represents a node in the trie, containing a map of child nodes and a boolean flag to mark if it's the end of a word.
- `SuffixTrie` represents the trie itself, with functions to insert a word into the trie and to search for a word.
- The `insert` function inserts a word into the trie character by character, creating new nodes as necessary.
- The `search` function traverses the trie to check if a given word exists in the trie.

This is a basic implementation. Depending on your use case, you might need to extend it with additional functionalities like deletion or handling special characters.

### 1. Algorithms & Data Structures (C++): Trie

A Trie, also known as a prefix tree, is a tree-like data structure used to efficiently store and retrieve a dynamic set of strings. It's particularly useful for tasks like auto-complete, spell checking, and searching for words with a common prefix. Each node of the trie represents a single character of the string. Here's a basic implementation of a Trie in C++:

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
public:
    TrieNode* root;

    Trie() {
        root = new TrieNode();
    }

    // Inserts a word into the trie.
    void insert(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                current->children[c] = new TrieNode();
            }
            current = current->children[c];
        }
        current->isEndOfWord = true;
    }

    // Returns true if the word is in the trie.
    bool search(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                return false;
            }
            current = current->children[c];
        }
        return current != nullptr && current->isEndOfWord;
    }

    // Returns true if there is any word in the trie that starts with the given prefix.
    bool startsWith(string prefix) {
        TrieNode* current = root;
        for (char c : prefix) {
            if (current->children.find(c) == current->children.end()) {
                return false;
            }
            current = current->children[c];
        }
        return current != nullptr;
    }
};

int main() {
    Trie trie;
    trie.insert("apple");
    cout << trie.search("apple") << endl;   // Output: 1 (true)
    cout << trie.search("app") << endl;     // Output: 0 (false)
    cout << trie.startsWith("app") << endl; // Output: 1 (true)
    trie.insert("app");
    cout << trie.search("app") << endl;     // Output: 1 (true)
    return 0;
}
```

In this implementation:

- Each node of the trie (`TrieNode`) contains an unordered map of its children nodes, representing characters of the alphabet, and a boolean flag indicating whether the node represents the end of a word.
- The `Trie` class provides methods to insert a word into the trie, search for a word, and check if there are any words with a given prefix.
- The `insert` function inserts a word character by character into the trie, creating new nodes as needed.
- The `search` function checks if a word exists in the trie by traversing it character by character.
- The `startsWith` function checks if there are any words in the trie that start with a given prefix.

### 1. Algorithms & Data Structures (C++): Trie Class

Sure! Below is a simple implementation of a Trie (also known as a prefix tree) class in C++. A Trie is a tree-like data structure used to store a dynamic set of strings, where the keys are usually strings. It allows for efficient retrieval of keys, usually in O(m) time complexity, where m is the length of the key.

```cpp
#include <iostream>
#include <unordered_map>
#include <string>

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

    // Insert a word into the Trie
    void insert(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                current->children[c] = new TrieNode();
            }
            current = current->children[c];
        }
        current->isEndOfWord = true;
    }

    // Search for a word in the Trie
    bool search(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                return false;
            }
            current = current->children[c];
        }
        return current != nullptr && current->isEndOfWord;
    }

    // Check if the given prefix exists in the Trie
    bool startsWith(string prefix) {
        TrieNode* current = root;
        for (char c : prefix) {
            if (current->children.find(c) == current->children.end()) {
                return false;
            }
            current = current->children[c];
        }
        return current != nullptr;
    }
};

// Example usage
int main() {
    Trie trie;
    trie.insert("apple");
    cout << (trie.search("apple") ? "Found" : "Not found") << endl; // Found
    cout << (trie.search("app") ? "Found" : "Not found") << endl;   // Not found
    cout << (trie.startsWith("app") ? "Prefix exists" : "Prefix does not exist") << endl; // Prefix exists
    trie.insert("app");
    cout << (trie.search("app") ? "Found" : "Not found") << endl;   // Found
    return 0;
}
```

In this implementation, each node of the Trie is represented by the `TrieNode` class, which contains a map of characters to `TrieNode` pointers representing the children of the node, and a boolean flag `isEndOfWord` indicating if the current node represents the end of a word.

The `Trie` class provides methods to insert a word into the Trie (`insert`), search for a word in the Trie (`search`), and check if a given prefix exists in the Trie (`startsWith`).

You can test this implementation by creating a `Trie` object and using its methods to insert words, search for words, or check if a prefix exists.

### 1. Algorithms & Data Structures (C++): Trie Data Structure

A Trie, also known as a prefix tree, is a tree-like data structure that is used to store a dynamic set of strings where each node represents a common prefix of its children. This makes it particularly efficient for tasks like searching for strings with a given prefix. Trie is widely used in tasks related to string manipulation and search, such as auto-completion systems and spell checkers.

Here's a basic implementation of a Trie in C++:

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

    void insert(string word) {
        TrieNode* curr = root;
        for (char c : word) {
            if (curr->children.find(c) == curr->children.end()) {
                curr->children[c] = new TrieNode();
            }
            curr = curr->children[c];
        }
        curr->isEndOfWord = true;
    }

    bool search(string word) {
        TrieNode* curr = root;
        for (char c : word) {
            if (curr->children.find(c) == curr->children.end()) {
                return false;
            }
            curr = curr->children[c];
        }
        return curr->isEndOfWord;
    }

    bool startsWith(string prefix) {
        TrieNode* curr = root;
        for (char c : prefix) {
            if (curr->children.find(c) == curr->children.end()) {
                return false;
            }
            curr = curr->children[c];
        }
        return true;
    }
};

int main() {
    Trie trie;
    trie.insert("apple");
    cout << (trie.search("apple") ? "Found" : "Not found") << endl; // Found
    cout << (trie.search("app") ? "Found" : "Not found") << endl;   // Not found
    cout << (trie.startsWith("app") ? "Found" : "Not found") << endl; // Found
    trie.insert("app");
    cout << (trie.search("app") ? "Found" : "Not found") << endl;   // Found
    return 0;
}
```

In this implementation:

- `TrieNode` represents a single node in the Trie. It contains a map of child nodes and a boolean flag `isEndOfWord` to indicate if the current node represents the end of a word.
- `Trie` class represents the Trie data structure. It has methods to insert a word into the Trie, search for a word, and check if a word starts with a given prefix.
- In the `insert` method, each character of the word is inserted as a child node of the current node if it doesn't exist already.
- In the `search` method, it traverses the Trie, character by character, and returns true if it reaches the end of the word.
- In the `startsWith` method, it traverses the Trie to check if the given prefix exists in the Trie.

This is a basic implementation of a Trie. Depending on your requirements, you might need to extend it with additional functionalities or optimizations.

### 1. Algorithms & Data Structures (C++): Trie Insertion

Sure, I can help with that. A Trie, also known as a prefix tree, is a tree-like data structure used for efficient retrieval of a key in a large set of strings. Here's how you can implement the insertion operation for a Trie in C++:

```cpp
#include <iostream>
#include <unordered_map>
using namespace std;

// Trie Node
class TrieNode {
public:
    unordered_map<char, TrieNode*> children;
    bool isEndOfWord;

    TrieNode() {
        isEndOfWord = false;
    }
};

// Trie class
class Trie {
public:
    TrieNode* root;

    Trie() {
        root = new TrieNode();
    }

    // Insert a word into the Trie
    void insert(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                current->children[c] = new TrieNode();
            }
            current = current->children[c];
        }
        current->isEndOfWord = true;
    }

    // Search for a word in the Trie
    bool search(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                return false; // Character not found
            }
            current = current->children[c];
        }
        return current != nullptr && current->isEndOfWord;
    }
};

int main() {
    Trie trie;

    // Insert some words
    trie.insert("hello");
    trie.insert("world");
    trie.insert("trie");
    trie.insert("tree");

    // Search for words
    cout << "Search results:" << endl;
    cout << "hello: " << (trie.search("hello") ? "Found" : "Not Found") << endl;
    cout << "world: " << (trie.search("world") ? "Found" : "Not Found") << endl;
    cout << "algorithm: " << (trie.search("algorithm") ? "Found" : "Not Found") << endl;

    return 0;
}
```

In this implementation, each node of the Trie is represented by the `TrieNode` class, which contains an unordered map of characters to child nodes and a boolean flag indicating whether the node represents the end of a word. The `Trie` class contains the root node and provides methods for insertion and searching.

The `insert` function iterates over each character of the word to be inserted, creating new nodes as needed and updating the `isEndOfWord` flag for the last character. The `search` function traverses the Trie to check if the given word exists in it.

You can run this code and test the insertion operation with your own set of words.

### 1. Algorithms & Data Structures (C++): Trie Queries

Implementing trie queries in C++ involves creating a trie data structure and then performing operations such as insertion, deletion, and searching. Here's a basic implementation:

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

    void deleteHelper(TrieNode* node) {
        if (!node) return;

        for (auto& pair : node->children) {
            deleteHelper(pair.second);
        }

        delete node;
    }

public:
    Trie() {
        root = new TrieNode();
    }

    void insert(string word) {
        TrieNode* current = root;
        for (char ch : word) {
            if (current->children.find(ch) == current->children.end()) {
                current->children[ch] = new TrieNode();
            }
            current = current->children[ch];
        }
        current->isEndOfWord = true;
    }

    bool search(string word) {
        TrieNode* current = root;
        for (char ch : word) {
            if (current->children.find(ch) == current->children.end()) {
                return false;
            }
            current = current->children[ch];
        }
        return current != nullptr && current->isEndOfWord;
    }

    void remove(string word) {
        removeHelper(root, word, 0);
    }

    void removeHelper(TrieNode* current, string& word, int index) {
        if (index == word.length()) {
            if (current->isEndOfWord) {
                current->isEndOfWord = false;
            }
            return;
        }

        char ch = word[index];
        if (current->children.find(ch) == current->children.end()) {
            return;
        }

        removeHelper(current->children[ch], word, index + 1);

        if (current->children[ch]->children.empty() && !current->children[ch]->isEndOfWord) {
            delete current->children[ch];
            current->children.erase(ch);
        }
    }

    ~Trie() {
        deleteHelper(root);
    }
};

int main() {
    Trie trie;
    trie.insert("apple");
    cout << (trie.search("apple") ? "Found" : "Not found") << endl;
    cout << (trie.search("app") ? "Found" : "Not found") << endl;
    trie.insert("app");
    cout << (trie.search("app") ? "Found" : "Not found") << endl;
    trie.remove("app");
    cout << (trie.search("app") ? "Found" : "Not found") << endl;

    return 0;
}
```

This implementation defines two classes: `TrieNode` and `Trie`. `TrieNode` represents a node in the trie, which has a map to store its children nodes and a boolean flag to indicate if it marks the end of a word. `Trie` class implements the trie data structure with operations like insertion, searching, and deletion.

Feel free to expand this implementation to support more operations or optimize it further based on your requirements!

### 1. Algorithms & Data Structures (C++): Trie Searching

Trie, also known as prefix tree, is a tree-like data structure that is used for efficiently storing and searching strings in a way that supports fast retrieval. Each node in a trie represents a common prefix of a set of strings. Trie searching involves looking for strings or patterns within the trie structure.

Here's an overview of how you can implement trie searching in C++:

1. **Trie Node Structure**: Define a structure for trie nodes. Each node will contain a boolean flag to indicate whether it marks the end of a word, and a collection of child nodes (usually implemented using a map or an array).

2. **Insertion**: Write a function to insert a string into the trie. Traverse the trie, creating nodes as necessary.

3. **Searching**: Implement a function to search for a string in the trie. Traverse the trie, checking if each character exists in the current node's children. If at any point a character is not found, the search fails. Additionally, check if the node marking the end of a word is reached.

4. **Prefix Search**: You can also implement prefix search functionality to find all strings in the trie that start with a given prefix.

Here's a basic example of a Trie implementation in C++:

```cpp
#include <iostream>
#include <unordered_map>
#include <string>

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
public:
    TrieNode* root;

    Trie() {
        root = new TrieNode();
    }

    // Insert a word into the trie
    void insert(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                current->children[c] = new TrieNode();
            }
            current = current->children[c];
        }
        current->isEndOfWord = true;
    }

    // Search for a word in the trie
    bool search(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                return false;
            }
            current = current->children[c];
        }
        return current->isEndOfWord;
    }

    // Search for words with a given prefix
    bool startsWith(string prefix) {
        TrieNode* current = root;
        for (char c : prefix) {
            if (current->children.find(c) == current->children.end()) {
                return false;
            }
            current = current->children[c];
        }
        return true;
    }
};

int main() {
    Trie trie;
    trie.insert("apple");
    cout << (trie.search("apple") ? "Found" : "Not found") << endl;   // Output: Found
    cout << (trie.search("app") ? "Found" : "Not found") << endl;     // Output: Not found
    cout << (trie.startsWith("app") ? "Found" : "Not found") << endl; // Output: Found
    return 0;
}
```

This example demonstrates how to insert words into the trie, search for complete words, and check for the existence of words with a given prefix. You can expand upon this basic implementation to add more functionalities or optimize for specific use cases.

### 1. Algorithms & Data Structures (C++): Trie: Hotel Reviews

Implementing a Trie for hotel reviews can be useful for tasks like efficient searching for hotels based on user reviews. In this scenario, each node of the Trie represents a character in a word, and the path from the root to a node represents a sequence of characters forming a word.

Here's a basic implementation of a Trie in C++ for hotel reviews:

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

    // Insert a word into the Trie
    void insert(const string& word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                current->children[c] = new TrieNode();
            }
            current = current->children[c];
        }
        current->isEndOfWord = true;
    }

    // Search for a word in the Trie
    bool search(const string& word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                return false;
            }
            current = current->children[c];
        }
        return current != nullptr && current->isEndOfWord;
    }
};

int main() {
    Trie hotelReviews;

    // Insert some reviews
    hotelReviews.insert("great");
    hotelReviews.insert("location");
    hotelReviews.insert("good");
    hotelReviews.insert("service");

    // Search for reviews
    cout << "Is 'great' in the reviews? " << (hotelReviews.search("great") ? "Yes" : "No") << endl;
    cout << "Is 'food' in the reviews? " << (hotelReviews.search("food") ? "Yes" : "No") << endl;

    return 0;
}
```

This code creates a basic Trie structure and demonstrates how to insert words (hotel review keywords) into the Trie and how to search for words within it. You can extend this implementation further according to your specific requirements, such as adding functionalities for prefix matching or storing additional information associated with each word.

### 1. Algorithms & Data Structures (C++): Trie: Shortest Unique Prefix

The "Shortest Unique Prefix" problem involves finding the shortest prefix of each string in a given set of strings such that no two strings have the same prefix. This can be efficiently solved using a Trie data structure.

Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;

class TrieNode {
public:
    unordered_map<char, TrieNode*> children;
    int count; // Number of times this node is visited

    TrieNode() : count(0) {}
};

class Trie {
public:
    TrieNode* root;

    Trie() {
        root = new TrieNode();
    }

    void insert(const string& word) {
        TrieNode* node = root;
        for (char ch : word) {
            if (node->children.find(ch) == node->children.end()) {
                node->children[ch] = new TrieNode();
            }
            node = node->children[ch];
            node->count++;
        }
    }

    string findShortestUniquePrefix(const string& word) {
        TrieNode* node = root;
        string prefix;
        for (char ch : word) {
            prefix += ch;
            node = node->children[ch];
            if (node->count == 1) // Found the unique prefix
                return prefix;
        }
        return ""; // Should never reach here if word is in the Trie
    }
};

vector<string> findShortestUniquePrefixes(const vector<string>& words) {
    Trie trie;
    for (const string& word : words) {
        trie.insert(word);
    }

    vector<string> result;
    for (const string& word : words) {
        result.push_back(trie.findShortestUniquePrefix(word));
    }
    return result;
}

int main() {
    vector<string> words = {"zebra", "dog", "duck", "dove"};
    vector<string> prefixes = findShortestUniquePrefixes(words);
    for (int i = 0; i < words.size(); ++i) {
        cout << "Shortest unique prefix of " << words[i] << ": " << prefixes[i] << endl;
    }
    return 0;
}
```

This code defines a Trie data structure and implements the `insert` method to insert words into the Trie and the `findShortestUniquePrefix` method to find the shortest unique prefix of a given word. The `findShortestUniquePrefixes` function iterates over all words in the input vector and finds their shortest unique prefixes. Finally, in the `main` function, you can see an example usage of this algorithm.

### 1. Algorithms & Data Structures (C++): Tries

Tries, also known as prefix trees, are tree-like data structures commonly used for storing and searching for strings in a way that allows for efficient retrieval of words with a common prefix. Each node in a trie represents a single character of a string, and paths from the root to the leaf nodes represent sequences of characters.

Here's a basic implementation of a trie in C++:

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
public:
    TrieNode* root;

    Trie() {
        root = new TrieNode();
    }

    void insert(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                current->children[c] = new TrieNode();
            }
            current = current->children[c];
        }
        current->isEndOfWord = true;
    }

    bool search(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                return false;
            }
            current = current->children[c];
        }
        return current->isEndOfWord;
    }

    bool startsWith(string prefix) {
        TrieNode* current = root;
        for (char c : prefix) {
            if (current->children.find(c) == current->children.end()) {
                return false;
            }
            current = current->children[c];
        }
        return true;
    }
};

int main() {
    Trie trie;
    trie.insert("apple");
    cout << (trie.search("apple") ? "Found" : "Not Found") << endl;   // Output: Found
    cout << (trie.search("app") ? "Found" : "Not Found") << endl;     // Output: Not Found
    cout << (trie.startsWith("app") ? "Found" : "Not Found") << endl; // Output: Found
    trie.insert("app");
    cout << (trie.search("app") ? "Found" : "Not Found") << endl;     // Output: Found
    return 0;
}
```

In this implementation:

- `TrieNode` represents each node in the trie. It contains an unordered map that maps characters to their corresponding child nodes and a boolean flag to indicate whether the node represents the end of a word.
- `Trie` represents the trie itself and contains operations like insertion, search, and prefix search (`startsWith`).

This implementation provides a basic framework for a trie data structure. Depending on your requirements, you may want to extend it with additional functionality or optimizations.

### 1. Algorithms & Data Structures (C++): Tries - Interview Question - Implement Prefix Trie

Implementing a prefix trie (also known as a "Trie" or "Prefix Tree") is a common interview question. In C++, you can create a Trie using a node-based approach. Each node represents a character, and children of a node represent the characters that can follow it in the trie. Here's a basic implementation:

```cpp
#include <iostream>
#include <unordered_map>
#include <string>

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
public:
    TrieNode* root;

    Trie() {
        root = new TrieNode();
    }

    void insert(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                current->children[c] = new TrieNode();
            }
            current = current->children[c];
        }
        current->isEndOfWord = true;
    }

    bool search(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                return false;
            }
            current = current->children[c];
        }
        return current->isEndOfWord;
    }

    bool startsWith(string prefix) {
        TrieNode* current = root;
        for (char c : prefix) {
            if (current->children.find(c) == current->children.end()) {
                return false;
            }
            current = current->children[c];
        }
        return true;
    }
};

int main() {
    Trie trie;

    trie.insert("apple");
    trie.insert("banana");
    trie.insert("app");

    cout << boolalpha;
    cout << "Search 'apple': " << trie.search("apple") << endl; // Output: true
    cout << "Search 'app': " << trie.search("app") << endl;     // Output: true
    cout << "Search 'ban': " << trie.search("ban") << endl;     // Output: false
    cout << "Starts with 'app': " << trie.startsWith("app") << endl; // Output: true
    cout << "Starts with 'ban': " << trie.startsWith("ban") << endl; // Output: true

    return 0;
}
```

In this implementation:

- `TrieNode` represents each node in the Trie. It has an unordered map to store children nodes and a boolean flag to mark the end of a word.
- `Trie` class implements the Trie data structure. It has a root node and methods to insert a word, search for a word, and check if a word starts with a given prefix.
- In the `insert` method, we iterate through each character of the word and create nodes if they don't exist already.
- In the `search` method, we traverse the Trie to find if the word exists.
- In the `startsWith` method, we traverse the Trie to check if a prefix exists.

### 1. Algorithms & Data Structures (C++): Tries & Pattern Matching Problems

Tries, also known as digital trees or prefix trees, are tree-like data structures used for efficient retrieval of keys in a large dataset of strings. They're particularly useful for solving pattern matching problems and are commonly employed in tasks like autocomplete, spell checking, and searching in text. In C++, you can implement tries using pointers or arrays.

Here's a basic implementation of a trie in C++:

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
public:
    TrieNode* root;

    Trie() {
        root = new TrieNode();
    }

    void insert(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                current->children[c] = new TrieNode();
            }
            current = current->children[c];
        }
        current->isEndOfWord = true;
    }

    bool search(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                return false;
            }
            current = current->children[c];
        }
        return current->isEndOfWord;
    }

    bool startsWith(string prefix) {
        TrieNode* current = root;
        for (char c : prefix) {
            if (current->children.find(c) == current->children.end()) {
                return false;
            }
            current = current->children[c];
        }
        return true;
    }
};

int main() {
    Trie trie;
    trie.insert("apple");
    cout << (trie.search("apple") ? "Found" : "Not found") << endl;   // Output: Found
    cout << (trie.search("app") ? "Found" : "Not found") << endl;     // Output: Not found
    cout << (trie.startsWith("app") ? "Starts with" : "Doesn't start with") << endl;  // Output: Starts with
    return 0;
}
```

This is a basic implementation of a trie supporting insertion, search, and prefix search operations. You can extend it to suit your specific needs, such as implementing deletion or additional operations.

For pattern matching problems, tries are commonly used in algorithms like Aho-Corasick algorithm for efficient string matching in a set of patterns.

If you have any specific questions or need further clarification, feel free to ask!

### 1. Algorithms & Data Structures (C++): Tries MCQ

Sure, I can help with that! Here are some multiple-choice questions on algorithms and data structures related to tries in C++:

1. What is a trie data structure primarily used for?
   a) Sorting
   b) Searching
   c) Storing integers
   d) Storing floating-point numbers

2. In a trie, each node typically represents:
   a) A character
   b) A string
   c) A number
   d) An array

3. Which of the following is NOT a common application of tries?
   a) Spell checking
   b) Autocomplete
   c) Text compression
   d) IP routing

4. What is the time complexity of searching in a trie with n keys?
   a) O(n)
   b) O(log n)
   c) O(m), where m is the length of the key
   d) O(1)

5. What is the space complexity of a trie?
   a) O(n)
   b) O(log n)
   c) O(m * n), where m is the average length of the keys and n is the number of keys
   d) O(1)

6. Which operation is efficient in a trie for deleting a key?
   a) O(1)
   b) O(log n)
   c) O(m), where m is the length of the key
   d) O(n)

7. Which data structure can be used to implement a trie efficiently?
   a) Array
   b) Linked List
   c) Hash Table
   d) Stack

8. In a trie, what does each edge represent?
   a) A character
   b) A string
   c) A number
   d) A pointer

9. What is the main advantage of using a trie over other data structures like hash tables?
   a) Faster search operations
   b) Lower space complexity
   c) Easier implementation
   d) Better cache locality

10. Which of the following operations can be performed efficiently using a trie?
    a) Finding the maximum element
    b) Finding the median
    c) Finding the minimum element
    d) Finding the average

### 1. Algorithms & Data Structures (C++): Tries Prefix Trie

A Trie, also known as a Prefix Tree, is a tree-like data structure that stores a dynamic set of strings, where the keys usually are sequences of characters. It allows for fast retrieval of stored values associated with keys, as well as efficient prefix searches. Here's a basic implementation of a Trie in C++:

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

    void insert(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                current->children[c] = new TrieNode();
            }
            current = current->children[c];
        }
        current->isEndOfWord = true;
    }

    bool search(string word) {
        TrieNode* current = root;
        for (char c : word) {
            if (current->children.find(c) == current->children.end()) {
                return false;
            }
            current = current->children[c];
        }
        return current->isEndOfWord;
    }

    bool startsWith(string prefix) {
        TrieNode* current = root;
        for (char c : prefix) {
            if (current->children.find(c) == current->children.end()) {
                return false;
            }
            current = current->children[c];
        }
        return true;
    }
};

int main() {
    Trie trie;
    trie.insert("apple");
    cout << (trie.search("apple") ? "Found" : "Not Found") << endl; // Output: Found
    cout << (trie.search("app") ? "Found" : "Not Found") << endl;   // Output: Not Found
    cout << (trie.startsWith("app") ? "Starts with" : "Doesn't start with") << endl; // Output: Starts with
    return 0;
}
```

This implementation provides basic functionalities like insertion of words, searching for complete words, and checking if a prefix exists in the Trie.

### 1. Algorithms & Data Structures (C++): What is a Trie? Why we need it?

A Trie, also known as a prefix tree, is a tree-like data structure used to store a dynamic set of strings where each node in the tree represents a common prefix of its descendant leaves.

Here's how it works:

- Each node in the Trie represents a single character of the string.
- Paths from the root to the leaves represent sequences of characters forming words.
- Nodes may have links to other nodes, typically one for each possible character.
- The structure of the Trie allows for efficient retrieval of strings, especially for tasks like searching for words with a common prefix.

Tries are particularly useful in tasks such as:

1. **String Search**: Tries provide fast lookup for strings, especially when you need to search for strings based on their prefixes.
2. **Auto-Completion**: They're commonly used in search engines and text editors for auto-completion suggestions as users type.
3. **Dictionary Implementation**: They're great for implementing dictionaries or storing a large number of words efficiently.
4. **IP Routing Tables**: Tries can be used to efficiently store and look up IP addresses and routing information in networking applications.

In C++, you can implement a Trie using pointers or arrays, where each node represents a character and has pointers to its child nodes. Tries are space-efficient for storing large sets of strings, especially when the strings share common prefixes.

### 1. Algorithms & Data Structures (C++): Biggest XOR

To find the maximum XOR value of any two elements in an array, you can use a Trie data structure. Here's a C++ implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Trie Node
struct TrieNode {
    TrieNode* children[2]; // For 0 and 1
    TrieNode() {
        children[0] = nullptr;
        children[1] = nullptr;
    }
};

// Trie class
class Trie {
public:
    TrieNode* root;
    Trie() {
        root = new TrieNode();
    }

    // Insert a number into the Trie
    void insert(int num) {
        TrieNode* curr = root;
        for (int i = 31; i >= 0; i--) {
            int bit = (num >> i) & 1;
            if (!curr->children[bit]) {
                curr->children[bit] = new TrieNode();
            }
            curr = curr->children[bit];
        }
    }

    // Find the maximum XOR value for a given number
    int findMaxXOR(int num) {
        TrieNode* curr = root;
        int maxXOR = 0;
        for (int i = 31; i >= 0; i--) {
            int bit = (num >> i) & 1;
            int oppositeBit = 1 - bit;
            if (curr->children[oppositeBit]) {
                maxXOR |= (1 << i); // Set ith bit
                curr = curr->children[oppositeBit];
            } else {
                curr = curr->children[bit];
            }
        }
        return maxXOR;
    }
};

// Function to find the maximum XOR value in an array
int findMaximumXOR(vector<int>& nums) {
    Trie trie;
    for (int num : nums) {
        trie.insert(num);
    }
    int maxXOR = 0;
    for (int num : nums) {
        maxXOR = max(maxXOR, trie.findMaxXOR(num));
    }
    return maxXOR;
}

int main() {
    vector<int> nums = {3, 10, 5, 25, 2, 8};
    cout << "Maximum XOR value: " << findMaximumXOR(nums) << endl;
    return 0;
}
```

This code creates a Trie data structure to efficiently store and search for numbers in binary form. The `findMaximumXOR` function iterates through the array of numbers, inserting each number into the Trie and simultaneously calculating the maximum XOR value. Finally, it returns the maximum XOR value found.

### 1. Algorithms & Data Structures (C++): Biggest XOR (Trie + Bitmasks)

Sure, let's dive into implementing the "Biggest XOR" problem using Trie and Bitmasks in C++. The problem statement typically goes like this: Given an array of integers, find the maximum XOR of any two elements.

Here's a step-by-step implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Trie node structure
struct TrieNode {
    TrieNode* children[2]; // 0 and 1
    TrieNode() {
        children[0] = nullptr;
        children[1] = nullptr;
    }
};

// Trie class
class Trie {
public:
    TrieNode* root;

    Trie() {
        root = new TrieNode();
    }

    // Insert an integer into the trie
    void insert(int num) {
        TrieNode* curr = root;
        for (int i = 31; i >= 0; i--) {
            int bit = (num >> i) & 1;
            if (curr->children[bit] == nullptr)
                curr->children[bit] = new TrieNode();
            curr = curr->children[bit];
        }
    }

    // Find the maximum XOR of num with any integer in the trie
    int findMaxXOR(int num) {
        TrieNode* curr = root;
        int maxXOR = 0;
        for (int i = 31; i >= 0; i--) {
            int bit = (num >> i) & 1;
            int oppositeBit = 1 - bit; // We are trying to maximize the XOR
            if (curr->children[oppositeBit] != nullptr) {
                maxXOR |= (1 << i); // Set the bit at position i
                curr = curr->children[oppositeBit];
            } else {
                curr = curr->children[bit];
            }
        }
        return maxXOR;
    }
};

// Function to find the maximum XOR of any two elements in the array
int findMaximumXOR(vector<int>& nums) {
    Trie trie;
    int maxXOR = 0;

    // Insert each number into the trie and find the maximum XOR
    for (int num : nums) {
        trie.insert(num);
        maxXOR = max(maxXOR, trie.findMaxXOR(num));
    }

    return maxXOR;
}

int main() {
    vector<int> nums = {3, 10, 5, 25, 2, 8};
    cout << "Maximum XOR: " << findMaximumXOR(nums) << endl;
    return 0;
}
```

This code uses a Trie data structure to efficiently find the maximum XOR. The time complexity of this solution is O(n * max_num_bits), where n is the number of elements in the array and max_num_bits is the maximum number of bits needed to represent any number in the array.
