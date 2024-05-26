# Backtracking

## General

### 1. Algorithms & Data Structures (C++): Backtracking

Backtracking is a fundamental algorithmic technique used to solve problems recursively by trying to build a solution incrementally, one piece at a time, and then backing off when you find that you're on the wrong path. It's especially useful for solving problems where you need to make a series of decisions, and each decision leads you to a new set of choices.

In C++, you can implement backtracking using recursion. Here's a general outline of how a backtracking algorithm might look:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to check if the current partial solution is valid
bool isSafe(/* arguments */) {
    // Implement your safety checks here
    return true; // Return true if the solution is valid, false otherwise
}

// Backtracking function
void backtrack(/* arguments */) {
    // Base case: If a solution is found, process it (or print it)
    if (/* base case condition */) {
        // Process the solution
        return;
    }

    // Iterate over all possible choices for the next decision
    for (/* iterate over choices */) {
        // Make a choice
        // Update the state

        // Check if the current partial solution is valid
        if (isSafe(/* arguments */)) {
            // Recur to the next step
            backtrack(/* arguments */);

            // Backtrack: Undo the choice and remove it from the state
        }
        // Undo the choice (backtrack)
    }
}

// Wrapper function to call the backtracking function with appropriate parameters
void solveProblem(/* arguments */) {
    // Initialize necessary variables
    // Call the backtracking function with appropriate initial parameters
    backtrack(/* initial arguments */);
}

int main() {
    // Call the function to solve the problem
    solveProblem(/* arguments */);

    return 0;
}
```

In this outline:

1. The `backtrack()` function represents the core of the backtracking algorithm. It's called recursively to explore all possible solutions by making decisions and exploring further until a valid solution is found or all possibilities are exhausted.

2. Inside the `backtrack()` function, you make a choice and proceed with the exploration. If the current partial solution is valid (`isSafe()` function returns true), you recur to explore further. If the solution is not valid, or if you reach a dead end, you backtrack by undoing the last choice and trying a different one.

3. The `isSafe()` function checks whether the current partial solution satisfies the problem's constraints. You need to implement this function according to the specific problem you're solving.

4. The `solveProblem()` function serves as a wrapper function to set up any necessary initial variables and parameters before calling `backtrack()`.

5. Finally, in the `main()` function, you call `solveProblem()` with appropriate arguments to start the backtracking process.

This is just a basic template, and the actual implementation will vary depending on the specific problem you're solving. You'll need to customize the template by filling in the details specific to your problem, such as the decision-making process, constraints, and how you process or output the valid solutions.

### 1. Algorithms & Data Structures (C++): Backtracking - Interview Question - Sudoku Solver (Hard)

Sure, solving Sudoku using backtracking is a classic interview question that demonstrates your understanding of both backtracking algorithms and basic data structures. Here's a C++ implementation:

```cpp
#include <iostream>
#include <vector>
using namespace std;

const int N = 9;

// Function to check if it's safe to place a number in the cell
bool isSafe(vector<vector<int>>& board, int row, int col, int num) {
    // Check if the number is not already present in the current row, column, and 3x3 subgrid
    for (int i = 0; i < N; ++i) {
        if (board[row][i] == num || board[i][col] == num || board[3 * (row / 3) + i / 3][3 * (col / 3) + i % 3] == num) {
            return false;
        }
    }
    return true;
}

// Function to solve Sudoku recursively
bool solveSudoku(vector<vector<int>>& board) {
    int row = -1, col = -1;
    bool isEmpty = true;

    // Find an empty cell
    for (int i = 0; i < N && isEmpty; ++i) {
        for (int j = 0; j < N && isEmpty; ++j) {
            if (board[i][j] == 0) {
                row = i;
                col = j;
                isEmpty = false;
            }
        }
    }

    // If no empty cell is found, puzzle is solved
    if (isEmpty) {
        return true;
    }

    // Try placing numbers from 1 to 9
    for (int num = 1; num <= 9; ++num) {
        // Check if it's safe to place the number in the cell
        if (isSafe(board, row, col, num)) {
            // Place the number
            board[row][col] = num;

            // Recur to solve the rest of the puzzle
            if (solveSudoku(board)) {
                return true;
            }

            // If placing the number leads to an invalid solution, backtrack and try next number
            board[row][col] = 0;
        }
    }

    // If no number can be placed in the current cell, backtrack
    return false;
}

// Function to print the solved Sudoku
void printSudoku(vector<vector<int>>& board) {
    for (int i = 0; i < N; ++i) {
        for (int j = 0; j < N; ++j) {
            cout << board[i][j] << " ";
        }
        cout << endl;
    }
}

int main() {
    vector<vector<int>> board = {
        {5, 3, 0, 0, 7, 0, 0, 0, 0},
        {6, 0, 0, 1, 9, 5, 0, 0, 0},
        {0, 9, 8, 0, 0, 0, 0, 6, 0},
        {8, 0, 0, 0, 6, 0, 0, 0, 3},
        {4, 0, 0, 8, 0, 3, 0, 0, 1},
        {7, 0, 0, 0, 2, 0, 0, 0, 6},
        {0, 6, 0, 0, 0, 0, 2, 8, 0},
        {0, 0, 0, 4, 1, 9, 0, 0, 5},
        {0, 0, 0, 0, 8, 0, 0, 7, 9}
    };

    if (solveSudoku(board)) {
        cout << "Sudoku Solved Successfully:" << endl;
        printSudoku(board);
    } else {
        cout << "No solution exists." << endl;
    }

    return 0;
}
```

This code defines functions to check if it's safe to place a number in a particular cell (`isSafe`), solve the Sudoku puzzle using backtracking (`solveSudoku`), and print the solved Sudoku (`printSudoku`). In the `main` function, a sample Sudoku puzzle is defined and solved.

### 1. Algorithms & Data Structures (C++): Backtracking Algorithms

Backtracking algorithms are a fundamental part of algorithms and data structures, especially in problem-solving contexts where you need to find solutions incrementally, exploring different possibilities. In C++, backtracking is often implemented using recursion. Here's a basic overview of how backtracking algorithms work and how they are implemented in C++:

1. **What is Backtracking?**
   Backtracking is a technique for finding solutions to combinatorial problems, especially constraint satisfaction problems, by incrementally building candidates for the solution and abandoning a candidate ("backtracking") as soon as it determines that the candidate cannot possibly be completed to a valid solution.

2. **Common Applications:**
   - N-Queens Problem
   - Sudoku Solver
   - Knight's Tour Problem
   - Graph Coloring
   - Subset Sum
   - Hamiltonian Cycle
   - Maze Solving

3. **Basic Steps:**
   - Choose a candidate solution.
   - Explore all possible alternatives recursively.
   - If the current candidate cannot lead to a solution, backtrack and try another candidate.

4. **C++ Implementation:**
   - Typically, backtracking is implemented using recursive functions.
   - At each step, you make a choice and explore all possibilities.
   - If a choice leads to a solution, you accept it; otherwise, you backtrack.
   - The base case of the recursion is reaching a solution or a dead-end.

5. **Example: N-Queens Problem:**

   ```cpp
   #include <iostream>
   using namespace std;

   const int N = 8; // Board size

   // Function to print the board
   void printBoard(int board[N][N]) {
       for (int i = 0; i < N; i++) {
           for (int j = 0; j < N; j++)
               cout << board[i][j] << " ";
           cout << endl;
       }
   }

   // Function to check if a queen can be placed on board[row][col]
   bool isSafe(int board[N][N], int row, int col) {
       int i, j;

       // Check this row on left side
       for (i = 0; i < col; i++)
           if (board[row][i])
               return false;

       // Check upper diagonal on left side
       for (i = row, j = col; i >= 0 && j >= 0; i--, j--)
           if (board[i][j])
               return false;

       // Check lower diagonal on left side
       for (i = row, j = col; j >= 0 && i < N; i++, j--)
           if (board[i][j])
               return false;

       return true;
   }

   // Recursive function to solve N-Queens problem
   bool solveNQueens(int board[N][N], int col) {
       // If all queens are placed, return true
       if (col >= N)
           return true;

       // Consider this column and try placing this queen in all rows one by one
       for (int i = 0; i < N; i++) {
           if (isSafe(board, i, col)) {
               // Place this queen in board[i][col]
               board[i][col] = 1;

               // Recur to place the rest of the queens
               if (solveNQueens(board, col + 1))
                   return true;

               // If placing queen in board[i][col] doesn't lead to a solution, remove queen from board[i][col]
               board[i][col] = 0; // BACKTRACK
           }
       }
       // If the queen can't be placed in any row in this column, return false
       return false;
   }

   // Main function to solve N-Queens problem
   void solveNQueens() {
       int board[N][N] = {0};

       if (!solveNQueens(board, 0))
           cout << "Solution does not exist";
       else
           printBoard(board);
   }

   int main() {
       solveNQueens();
       return 0;
   }
   ```

This C++ code solves the N-Queens problem using backtracking. It's a good example of how backtracking works recursively, exploring all possible configurations until a solution is found or all possibilities are exhausted.

### 1. Algorithms & Data Structures (C++): Backtracking on Arrays

Backtracking is a powerful algorithmic technique used to systematically search for solutions to problems, especially in cases where brute-force approaches are impractical. It involves trying out different sequences of decisions, and if a decision leads to a dead end, it backs up and tries a different decision.

In the context of arrays in C++, backtracking can be used to solve a variety of problems such as subset sum, permutation, combination, sudoku solving, etc. Here's a basic example of how backtracking can be applied to find all subsets of an array:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Backtracking function to generate all subsets of an array
void backtrack(vector<int>& nums, int start, vector<int>& subset, vector<vector<int>>& subsets) {
    subsets.push_back(subset); // Add the current subset to the result

    // Iterate through the array starting from 'start' index
    for (int i = start; i < nums.size(); ++i) {
        subset.push_back(nums[i]); // Include current element in the subset
        // Recursively call backtrack to generate subsets with the current element
        backtrack(nums, i + 1, subset, subsets);
        subset.pop_back(); // Backtrack: remove the current element from the subset
    }
}

// Function to generate all subsets of an array
vector<vector<int>> generateSubsets(vector<int>& nums) {
    vector<vector<int>> subsets;
    vector<int> subset;
    backtrack(nums, 0, subset, subsets);
    return subsets;
}

int main() {
    vector<int> nums = {1, 2, 3};
    vector<vector<int>> subsets = generateSubsets(nums);
    
    // Print all subsets
    for (const auto& subset : subsets) {
        cout << "[";
        for (int num : subset) {
            cout << num << " ";
        }
        cout << "]" << endl;
    }
    
    return 0;
}
```

In this code:

- The `backtrack` function recursively generates all possible subsets of the input array `nums`. It starts from the `start` index and explores all possible combinations of elements.
- At each step, it includes the current element in the subset, recursively calls itself to explore further possibilities, and then removes the current element to backtrack.
- The `generateSubsets` function initializes the backtracking process and returns the list of generated subsets.
- In the `main` function, an example array `{1, 2, 3}` is used to demonstrate how to generate subsets.

This is a basic example, but backtracking can be used to solve more complex problems efficiently as well.

### 1. Algorithms & Data Structures (C++): Backtracking Problems

Backtracking is a powerful algorithmic technique used to solve problems by exploring all possible solutions. It works incrementally and systematically, constructing candidates for the solution, and discarding a candidate as soon as it determines that the candidate cannot possibly lead to a valid solution. Here are some classic backtracking problems in C++:

1. **N-Queens Problem**: Place N queens on an N×N chessboard such that no two queens attack each other.

2. **Sudoku Solver**: Given a partially filled 9×9 grid, fill the grid using the digits 1 to 9 such that every row, column, and 3×3 subgrid contains exactly one instance of the digits 1 to 9.

3. **Subset Sum**: Given a set of positive integers and a target sum, find all subsets that sum up to the target sum.

4. **Permutations**: Generate all permutations of a given sequence of numbers.

5. **Word Search**: Given a 2D board and a word, find if the word exists in the grid. The word can be constructed from letters of sequentially adjacent cells, where "adjacent" cells are horizontally or vertically neighboring.

Here's a simplified example of solving the N-Queens problem in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

bool isSafe(vector<vector<int>>& board, int row, int col, int N) {
    // Check if there is a queen in the same column
    for (int i = 0; i < row; ++i)
        if (board[i][col])
            return false;

    // Check upper left diagonal
    for (int i = row, j = col; i >= 0 && j >= 0; --i, --j)
        if (board[i][j])
            return false;

    // Check upper right diagonal
    for (int i = row, j = col; i >= 0 && j < N; --i, ++j)
        if (board[i][j])
            return false;

    return true;
}

bool solveNQueensUtil(vector<vector<int>>& board, int row, int N) {
    if (row >= N)
        return true;

    for (int i = 0; i < N; ++i) {
        if (isSafe(board, row, i, N)) {
            board[row][i] = 1; // Place the queen

            if (solveNQueensUtil(board, row + 1, N))
                return true;

            // Backtrack
            board[row][i] = 0;
        }
    }
    return false;
}

void solveNQueens(int N) {
    vector<vector<int>> board(N, vector<int>(N, 0));
    if (solveNQueensUtil(board, 0, N)) {
        for (int i = 0; i < N; ++i) {
            for (int j = 0; j < N; ++j) {
                cout << board[i][j] << " ";
            }
            cout << endl;
        }
    } else {
        cout << "No solution exists" << endl;
    }
}

int main() {
    int N = 4;
    solveNQueens(N);
    return 0;
}
```

This code solves the N-Queens problem for a 4x4 chessboard. You can modify the `N` variable to solve it for different board sizes.

### 1. Algorithms & Data Structures (C++): Backtracking Template

Sure, here's a basic template for backtracking in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void backtrack(vector<int>& nums, vector<int>& path, vector<vector<int>>& result) {
    // Base case: if the path is a solution, add it to the result
    if (/* condition to check if path is a solution */) {
        result.push_back(path);
        return;
    }

    // Iterate over all possible choices for the next element
    for (int i = 0; i < nums.size(); ++i) {
        // Skip if the current choice is not valid (optional pruning)
        if (/* condition to check if current choice is valid */) {
            continue;
        }

        // Choose
        path.push_back(nums[i]);

        // Explore
        backtrack(nums, path, result);

        // Unchoose (backtrack)
        path.pop_back();
    }
}

vector<vector<int>> generateSubsets(vector<int>& nums) {
    vector<vector<int>> result;
    vector<int> path;
    backtrack(nums, path, result);
    return result;
}

int main() {
    vector<int> nums = {1, 2, 3};
    vector<vector<int>> subsets = generateSubsets(nums);
    // Print subsets
    for (const auto& subset : subsets) {
        cout << "[";
        for (int num : subset) {
            cout << num << " ";
        }
        cout << "]" << endl;
    }
    return 0;
}
```

This template demonstrates backtracking to generate all possible subsets of a given set of numbers. You can customize it for other problems by adjusting the base case condition, choices, and constraints in the `backtrack` function.

### 1. Algorithms & Data Structures (C++): Backtracking vs Brute Force Approach

Both backtracking and brute force are techniques used to solve problems, especially in the context of algorithms and data structures. Here's a breakdown of each approach:

1. **Brute Force Approach**:
   - Brute force is a straightforward approach where you try all possibilities and pick the best one.
   - It typically involves systematically checking all possible solutions until the correct one is found.
   - This approach can be simple to implement but can become impractical as the problem size grows due to its exponential time complexity.
   - It doesn't involve any specific strategy for pruning or eliminating unpromising paths.

2. **Backtracking Approach**:
   - Backtracking is a more intelligent, systematic way of searching for solutions, especially in problems involving choices.
   - It is based on recursion and is particularly useful for solving problems that have a large search space.
   - Backtracking involves exploring all possible solutions, but it abandons a solution as soon as it determines that it cannot lead to a valid solution.
   - It often uses a depth-first search strategy to explore the solution space, going as deep as possible before backtracking.
   - Backtracking algorithms can be more efficient than brute force because they avoid exploring parts of the solution space that cannot lead to a valid solution.
   - Examples of problems that can be efficiently solved using backtracking include the N-Queens problem, Sudoku, and the Knight's Tour problem.

In summary, while brute force involves exhaustively checking all possible solutions without much optimization, backtracking is a more refined approach that intelligently prunes the search space, making it more efficient, especially for problems with a large solution space. However, both approaches have their place depending on the problem at hand and the constraints involved.

### 1. Algorithms & Data Structures (C++): Backtracking: Backtracking Problems

Backtracking is a powerful algorithmic technique used to solve problems recursively by systematically searching through all possible solutions. It is particularly useful for solving problems that involve finding all possible configurations or subsets of a solution.

Here are some classic backtracking problems that you might encounter:

1. **N-Queens Problem**: Given an \( n \times n \) chessboard, place \( n \) queens on the board such that no two queens attack each other (i.e., no two queens share the same row, column, or diagonal).

2. **Subset Sum Problem**: Given a set of integers and a target sum, find all distinct subsets of the given set that sum up to the target sum.

3. **Permutations**: Generate all possible permutations of a given set of elements.

4. **Combination Sum**: Given a set of candidate numbers and a target number, find all unique combinations of candidates where the chosen numbers sum to the target.

5. **Sudoku Solver**: Given a partially filled \( 9 \times 9 \) Sudoku grid, fill the grid using digits 1 to 9 such that every row, column, and 3x3 subgrid contains all the digits from 1 to 9 without repetition.

6. **Word Search**: Given a 2D board of letters and a word, determine if the word exists in the grid. The word can be constructed from letters of sequentially adjacent cells, where "adjacent" cells are horizontally or vertically neighboring.

7. **Knight's Tour**: Given a chessboard of size \( n \times n \) and a starting position of a knight, find a sequence of moves such that the knight visits every square exactly once.

8. **Graph Coloring**: Given an undirected graph, assign colors to its vertices such that no two adjacent vertices have the same color.

These problems vary in complexity and require different strategies for backtracking. However, the basic approach involves exploring all possible solutions recursively and discarding those that do not satisfy the problem constraints. Additionally, pruning can be employed to avoid unnecessary exploration of certain paths. In many cases, efficient implementation of backtracking involves the use of recursion and careful management of state.

Would you like a deeper dive into any of these problems or perhaps some code examples in C++?

### 1. Algorithms & Data Structures (C++): Backtracking: Brute-force search and backtracking

Brute-force search and backtracking are fundamental techniques used in algorithms and data structures, particularly in solving combinatorial problems. Let's break down each of them:

#### Brute-force search

Brute-force search, also known as exhaustive search, is a straightforward method of solving a problem by systematically trying all possible solutions. It involves generating all possible candidates and checking each one to see if it satisfies the problem's conditions. While it's conceptually simple, brute-force search can be inefficient, especially for large problem spaces, as it explores every possible solution without considering the problem's structure.

#### Example

Consider the problem of finding all permutations of a given set of elements. A brute-force approach would generate all possible permutations and check each one against a condition (e.g., uniqueness).

#### Backtracking

Backtracking is an optimization technique used to solve problems with a large search space by incrementally building candidates for the solution and abandoning them if they cannot fulfill the conditions of the problem. It works by exploring a solution space recursively, incrementally building partial solutions and backtracking when it determines that a partial solution cannot be completed to a valid solution.

#### Example

Consider the problem of solving a Sudoku puzzle. Backtracking can be used to try different numbers for each cell, recursively exploring possible configurations until a solution is found or all possibilities are exhausted. If a configuration leads to a contradiction, the algorithm backtracks and tries a different approach.

#### Relationship between brute-force search and backtracking

Backtracking is often used in conjunction with brute-force search to reduce the search space by intelligently pruning branches of the search tree that cannot lead to a valid solution. While brute-force search explores all possible solutions without any guidance, backtracking employs a systematic approach to explore the search space more efficiently by avoiding paths that are guaranteed to be invalid.

#### Example

In the permutation problem mentioned earlier, backtracking can be used to generate permutations by swapping elements, but it would backtrack whenever it encounters a duplicate permutation or when it exhausts all possibilities for a particular position.

In C++, both brute-force search and backtracking can be implemented using recursion, where each recursive call explores a different part of the solution space.

Do you want to see a simple C++ implementation of a backtracking algorithm for a specific problem?

### 1. Algorithms & Data Structures (C++): Backtracking: Coloring problem

The coloring problem is a classic problem in graph theory and algorithm design. Given an undirected graph, the task is to assign colors to each vertex in such a way that no two adjacent vertices share the same color, using the fewest possible colors. Backtracking is one of the techniques commonly used to solve this problem efficiently. Here's how you can approach the coloring problem using backtracking in C++:

```cpp
#include <iostream>
#include <vector>
using namespace std;

#define V 4 // Number of vertices in the graph

bool isSafe(int v, vector<vector<int>>& graph, vector<int>& color, int c) {
    for (int i = 0; i < V; i++) {
        if (graph[v][i] && c == color[i]) // If an adjacent vertex has the same color
            return false;
    }
    return true;
}

bool graphColoringUtil(vector<vector<int>>& graph, int m, vector<int>& color, int v) {
    if (v == V)
        return true;

    for (int c = 1; c <= m; c++) {
        if (isSafe(v, graph, color, c)) {
            color[v] = c;

            if (graphColoringUtil(graph, m, color, v + 1))
                return true;

            color[v] = 0; // Backtrack
        }
    }
    return false;
}

bool graphColoring(vector<vector<int>>& graph, int m) {
    vector<int> color(V, 0); // Initialize all colors as 0

    if (!graphColoringUtil(graph, m, color, 0)) {
        cout << "Solution does not exist";
        return false;
    }

    // Print the solution
    cout << "Solution exists: The vertex colors are\n";
    for (int i = 0; i < V; i++)
        cout << "Vertex " << i << " ---> Color " << color[i] << endl;
    return true;
}

int main() {
    vector<vector<int>> graph = {{0, 1, 1, 1},
                                 {1, 0, 1, 0},
                                 {1, 1, 0, 1},
                                 {1, 0, 1, 0}};
    int m = 3; // Number of colors

    graphColoring(graph, m);
    return 0;
}
```

In this code:

- The `graph` represents the adjacency matrix of the input graph.
- `graphColoringUtil` is a recursive function that tries different colors for a vertex `v` and checks if the assignment of colors leads to a solution.
- `graphColoring` initializes colors and starts with vertex 0. If a solution is found, it prints the colors of vertices; otherwise, it prints that no solution exists.

You can modify the input graph and the number of colors according to your requirements. This algorithm efficiently solves the graph coloring problem using backtracking.

### 1. Algorithms & Data Structures (C++): Backtracking: Coloring problem implementation

Sure, I can provide you with a basic implementation of the graph coloring problem using backtracking in C++. The graph coloring problem involves coloring the vertices of a graph in such a way that no two adjacent vertices share the same color, using the fewest number of colors possible.

Here's a simple implementation:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

class Graph {
    int V; // Number of vertices
    vector<vector<int>> adj; // Adjacency list representation of graph

public:
    Graph(int v) : V(v) {
        adj.resize(V);
    }

    // Function to add an edge to the graph
    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    // Function to check if the current color assignment is safe for vertex v
    bool isSafe(int v, vector<int>& color, int c) {
        for (int u : adj[v]) {
            if (color[u] == c)
                return false;
        }
        return true;
    }

    // Function to recursively assign colors to vertices using backtracking
    bool graphColoringUtil(vector<int>& color, int v, int m) {
        if (v == V)
            return true;

        for (int c = 1; c <= m; ++c) {
            if (isSafe(v, color, c)) {
                color[v] = c;
                if (graphColoringUtil(color, v + 1, m))
                    return true;
                color[v] = 0; // Backtrack
            }
        }

        return false;
    }

    // Function to assign colors to vertices of the graph
    void graphColoring(int m) {
        vector<int> color(V, 0);
        if (graphColoringUtil(color, 0, m)) {
            cout << "Graph coloring possible with " << m << " colors:" << endl;
            for (int i = 0; i < V; ++i)
                cout << "Vertex " << i << " --> Color " << color[i] << endl;
        } else {
            cout << "Graph coloring not possible with " << m << " colors." << endl;
        }
    }
};

int main() {
    Graph g(4); // Example graph with 4 vertices
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 3);

    int m = 3; // Number of colors available
    g.graphColoring(m);

    return 0;
}
```

This implementation defines a `Graph` class with methods to add edges, check if a color assignment is safe, and perform graph coloring using backtracking. In the `main` function, an example graph with 4 vertices is created, and the `graphColoring` method is called with the number of colors available. You can modify the graph and the number of colors to test different scenarios.

### 1. Algorithms & Data Structures (C++): Backtracking: Knight's tour problem Knight's tour problem implementation

Sure, here's a simple implementation of the Knight's Tour problem using backtracking in C++:

```cpp
#include <iostream>
#include <vector>

#define N 8

using namespace std;

// Function to check if (x, y) is valid
// chessboard coordinates
bool isSafe(int x, int y, vector<vector<int>>& board) {
    return (x >= 0 && y >= 0 && x < N && y < N && board[x][y] == -1);
}

// Function to print the solution matrix
void printSolution(vector<vector<int>>& board) {
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++)
            cout << board[i][j] << " ";
        cout << endl;
    }
}

// Function to solve Knight Tour problem using
// backtracking
bool solveKTUtil(int x, int y, int movei, vector<vector<int>>& sol,
                 int xMove[], int yMove[]) {
    int k, next_x, next_y;
    if (movei == N * N)
        return true;

    // Try all next moves from the current coordinate x, y
    for (k = 0; k < 8; k++) {
        next_x = x + xMove[k];
        next_y = y + yMove[k];
        if (isSafe(next_x, next_y, sol)) {
            sol[next_x][next_y] = movei;
            if (solveKTUtil(next_x, next_y, movei + 1, sol, xMove, yMove))
                return true;
            else
                sol[next_x][next_y] = -1; // backtracking
        }
    }

    return false;
}

// Function to solve the Knight Tour problem
void solveKT() {
    vector<vector<int>> sol(N, vector<int>(N, -1));

    // Possible moves for a knight
    int xMove[8] = {2, 1, -1, -2, -2, -1, 1, 2};
    int yMove[8] = {1, 2, 2, 1, -1, -2, -2, -1};

    // Starting from (0,0)
    sol[0][0] = 0;

    // If solution doesn't exist
    if (!solveKTUtil(0, 0, 1, sol, xMove, yMove)) {
        cout << "Solution does not exist";
    } else {
        cout << "Solution:\n";
        printSolution(sol);
    }
}

int main() {
    // Function Call
    solveKT();
    return 0;
}
```

This code will find a solution for the Knight's Tour problem on a standard 8x8 chessboard. It uses backtracking to explore all possible paths and find a solution.

### 1. Algorithms & Data Structures (C++): Backtracking: N-queens problem

The N-queens problem is a classic problem in computer science and combinatorial optimization. It asks for a placement of N queens on an N×N chessboard such that no two queens threaten each other. In chess, a queen can attack any piece in the same row, column, or diagonal as itself.

One common approach to solve the N-queens problem is using backtracking. Here's how you can implement it in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to check if a queen can be placed at board[row][col]
bool isSafe(vector<string>& board, int row, int col, int n) {
    // Check the left side of the current row
    for (int i = 0; i < col; i++) {
        if (board[row][i] == 'Q') {
            return false;
        }
    }
    
    // Check upper diagonal on left side
    for (int i = row, j = col; i >= 0 && j >= 0; i--, j--) {
        if (board[i][j] == 'Q') {
            return false;
        }
    }
    
    // Check lower diagonal on left side
    for (int i = row, j = col; i < n && j >= 0; i++, j--) {
        if (board[i][j] == 'Q') {
            return false;
        }
    }
    
    return true;
}

// Recursive function to solve N-queens problem using backtracking
bool solveNQueensUtil(vector<string>& board, int col, int n, vector<vector<string>>& res) {
    // Base case: If all queens are placed, return true
    if (col >= n) {
        res.push_back(board);
        return true;
    }
    
    bool result = false;
    // Try placing a queen in each row of the current column
    for (int i = 0; i < n; i++) {
        if (isSafe(board, i, col, n)) {
            // Place the queen on the board
            board[i][col] = 'Q';
            
            // Recur to place the rest of the queens
            result = solveNQueensUtil(board, col + 1, n, res) || result;
            
            // If placing queen in board[i][col] doesn't lead to a solution,
            // then remove the queen from board[i][col]
            board[i][col] = '.';
        }
    }
    
    return result;
}

// Function to solve N-queens problem
vector<vector<string>> solveNQueens(int n) {
    vector<vector<string>> res;
    // Initialize the board
    vector<string> board(n, string(n, '.'));
    
    // Call recursive utility function to solve N-queens problem
    solveNQueensUtil(board, 0, n, res);
    
    return res;
}

// Function to print the solutions
void printSolutions(vector<vector<string>>& solutions) {
    int count = 1;
    for (auto& sol : solutions) {
        cout << "Solution " << count++ << ":\n";
        for (auto& row : sol) {
            cout << row << '\n';
        }
        cout << "\n";
    }
}

int main() {
    int n = 4; // Change n for different board sizes
    vector<vector<string>> solutions = solveNQueens(n);
    printSolutions(solutions);
    
    return 0;
}
```

This code will output all the possible solutions for the N-queens problem for a given N. You can change the value of `n` in the `main()` function to solve for different board sizes.

### 1. Algorithms & Data Structures (C++): Backtracking: N-queens problem and the stack memory

The N-Queens problem is a classic algorithmic problem where the task is to place N chess queens on an N×N chessboard in such a way that no two queens threaten each other. This means that no two queens share the same row, column, or diagonal.

Backtracking is a commonly used technique to solve such problems. It works by trying partial solutions and abandoning them when they are found to be invalid. It then backtracks to the previous decision point and tries a different option.

When implementing the N-Queens problem using backtracking in C++, you typically use a recursive approach. Each recursive call represents trying to place a queen in a particular row of the chessboard. If placing a queen in a particular position leads to a solution, you continue with the next row. If it doesn't, you backtrack and try a different position.

Here's a basic outline of how you might implement the N-Queens problem using backtracking in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

bool isSafe(vector<vector<int>>& board, int row, int col, int N) {
    // Check if there's a queen in the same column
    for (int i = 0; i < row; ++i)
        if (board[i][col])
            return false;

    // Check upper diagonal on the left side
    for (int i = row, j = col; i >= 0 && j >= 0; --i, --j)
        if (board[i][j])
            return false;

    // Check upper diagonal on the right side
    for (int i = row, j = col; i >= 0 && j < N; --i, ++j)
        if (board[i][j])
            return false;

    return true;
}

bool solveNQueensUtil(vector<vector<int>>& board, int row, int N) {
    if (row == N)
        return true;

    for (int col = 0; col < N; ++col) {
        if (isSafe(board, row, col, N)) {
            board[row][col] = 1;
            if (solveNQueensUtil(board, row + 1, N))
                return true;
            board[row][col] = 0; // backtrack
        }
    }

    return false;
}

void solveNQueens(int N) {
    vector<vector<int>> board(N, vector<int>(N, 0));

    if (solveNQueensUtil(board, 0, N)) {
        cout << "Solution exists. The board configuration is:\n";
        for (int i = 0; i < N; ++i) {
            for (int j = 0; j < N; ++j)
                cout << board[i][j] << " ";
            cout << "\n";
        }
    } else {
        cout << "No solution exists.\n";
    }
}

int main() {
    int N;
    cout << "Enter the size of the chessboard (N): ";
    cin >> N;
    solveNQueens(N);
    return 0;
}
```

In this implementation:

- The `isSafe` function checks if it's safe to place a queen in the given row and column.
- The `solveNQueensUtil` function is a recursive function that tries to place queens in each row of the chessboard.
- The `solveNQueens` function initializes the chessboard and calls `solveNQueensUtil` to solve the problem.
- Finally, in the `main` function, the user inputs the size of the chessboard, and the solution is printed if it exists.

Regarding the stack memory, backtracking algorithms like this one typically use the call stack extensively because of their recursive nature. Each recursive call consumes some stack memory. If the depth of recursion becomes too large, it may lead to a stack overflow error. However, for moderately sized N (e.g., N < 20), this implementation should work fine. If you want to handle larger values of N, you might need to implement an iterative solution or use techniques like memoization.

### 1. Algorithms & Data Structures (C++): Backtracking: N-queens problem implementation

Sure, I can provide you with a simple implementation of the N-queens problem using backtracking in C++. In this problem, you have to place N queens on an NxN chessboard in such a way that no two queens attack each other. Here's the implementation:

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to check if it's safe to place a queen at board[row][col]
bool isSafe(vector<vector<int>>& board, int row, int col, int N) {
    // Check if there's a queen in the same column
    for (int i = 0; i < row; ++i) {
        if (board[i][col] == 1)
            return false;
    }

    // Check upper left diagonal
    for (int i = row, j = col; i >= 0 && j >= 0; --i, --j) {
        if (board[i][j] == 1)
            return false;
    }

    // Check upper right diagonal
    for (int i = row, j = col; i >= 0 && j < N; --i, ++j) {
        if (board[i][j] == 1)
            return false;
    }

    return true;
}

// Function to solve N-queens problem using backtracking
bool solveNQueensUtil(vector<vector<int>>& board, int row, int N) {
    // Base case: If all queens are placed, return true
    if (row == N)
        return true;

    for (int col = 0; col < N; ++col) {
        // Check if it's safe to place a queen at board[row][col]
        if (isSafe(board, row, col, N)) {
            // Place the queen
            board[row][col] = 1;

            // Recur to place rest of the queens
            if (solveNQueensUtil(board, row + 1, N))
                return true;

            // If placing queen in board[row][col] doesn't lead to a solution, backtrack
            board[row][col] = 0; // Backtrack
        }
    }

    // If queen can't be placed in any column of this row, then return false
    return false;
}

// Function to solve N-queens problem
void solveNQueens(int N) {
    vector<vector<int>> board(N, vector<int>(N, 0));

    if (solveNQueensUtil(board, 0, N)) {
        // Print the solution
        for (int i = 0; i < N; ++i) {
            for (int j = 0; j < N; ++j) {
                cout << board[i][j] << " ";
            }
            cout << endl;
        }
    } else {
        cout << "Solution does not exist!";
    }
}

int main() {
    int N;
    cout << "Enter the number of queens (N): ";
    cin >> N;

    solveNQueens(N);

    return 0;
}
```

This code defines a function `solveNQueens` which takes an integer `N` as input representing the number of queens to be placed on the chessboard. It then initializes an empty chessboard represented by a 2D vector of integers. The function `solveNQueensUtil` is a helper function that uses backtracking to recursively try placing queens on the board. The function `isSafe` checks whether it is safe to place a queen at a given position on the board. Finally, the `main` function takes input from the user for the number of queens and calls the `solveNQueens` function to solve the problem and print the solution.

### 1. Algorithms & Data Structures (C++): Backtracking: What is the problem with backtracking?

Backtracking is a powerful technique used to systematically search through all possible solutions to a problem. However, it can also have some limitations and challenges:

1. **Exponential Time Complexity**: Backtracking algorithms typically have exponential time complexity because they explore all possible combinations of solutions. As the input size increases, the time taken to find a solution grows exponentially, making it impractical for large inputs.

2. **Space Complexity**: Backtracking algorithms often require additional memory to store the current state of the search, such as the current solution path or the state of variables. This can lead to high space complexity, especially for problems with deep search trees.

3. **Completeness**: Backtracking algorithms do not guarantee finding the optimal solution. They only find a solution if it exists within the search space. In some cases, the search space may be too large, and backtracking may not be able to explore all possible solutions in a reasonable amount of time.

4. **Inefficiency in Certain Cases**: Backtracking may not be the most efficient solution approach for certain types of problems. For example, problems with a highly constrained search space or problems that can be solved more efficiently using other techniques may not benefit from backtracking.

5. **Difficulty in Implementation and Debugging**: Backtracking algorithms can be complex to implement and debug, especially for problems with intricate constraints or branching factors. Keeping track of the current state and correctly pruning the search space requires careful attention to detail.

Despite these challenges, backtracking remains a valuable tool in the arsenal of algorithms and is widely used in various applications such as solving puzzles, generating permutations, and solving constraint satisfaction problems. However, it's essential to consider its limitations and explore alternative approaches when appropriate.

### 1. Algorithms & Data Structures (C++): Bactracking on Vectors

Backtracking is a powerful technique for solving combinatorial problems, and it can indeed be applied to problems involving vectors in C++. Here's a basic outline of how you can implement backtracking on vectors in C++:

1. **Define your problem**: Clearly define the problem you want to solve using backtracking and represent it in terms of vectors. For example, you might want to find all permutations of a vector, subsets of a vector, combinations, etc.

2. **Implement the backtracking function**: Write a recursive function that explores all possible solutions by trying different choices at each step and backtracking when a choice doesn't lead to a valid solution. This function will typically take the current state, the choices available at the current step, and additional parameters specific to your problem.

3. **Terminate conditions**: Define conditions under which the backtracking should stop, typically when a valid solution is found or when all possibilities have been explored.

4. **Main function**: In your main function, initialize necessary variables and call the backtracking function with appropriate parameters.

Here's a simple example of backtracking to find all permutations of a vector:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void backtrack(vector<int>& nums, vector<int>& curr, vector<bool>& used, vector<vector<int>>& result) {
    if (curr.size() == nums.size()) {
        result.push_back(curr);
        return;
    }
    for (int i = 0; i < nums.size(); ++i) {
        if (!used[i]) {
            curr.push_back(nums[i]);
            used[i] = true;
            backtrack(nums, curr, used, result);
            used[i] = false;
            curr.pop_back();
        }
    }
}

vector<vector<int>> permute(vector<int>& nums) {
    vector<vector<int>> result;
    vector<int> curr;
    vector<bool> used(nums.size(), false);
    backtrack(nums, curr, used, result);
    return result;
}

int main() {
    vector<int> nums = {1, 2, 3};
    vector<vector<int>> permutations = permute(nums);
    for (const auto& perm : permutations) {
        for (int num : perm) {
            cout << num << " ";
        }
        cout << endl;
    }
    return 0;
}
```

This code finds all permutations of a given vector of integers. The `backtrack` function explores all possible permutations recursively, while the `permute` function initializes necessary variables and calls the `backtrack` function. Finally, in the `main` function, we call `permute` with the input vector and print the resulting permutations.

### 1. Algorithms & Data Structures (C++): Combination Sum - Backtracking

Certainly! The Combination Sum problem is a classic algorithmic problem where you're given a set of candidate numbers (candidates) and a target number (target), and you need to find all unique combinations in candidates where the candidate numbers sum up to the target.

Here's a C++ implementation of the Combination Sum problem using backtracking:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void backtrack(vector<vector<int>>& res, vector<int>& candidates, vector<int>& combination, int target, int start) {
    if (target == 0) {
        res.push_back(combination);
        return;
    }

    for (int i = start; i < candidates.size() && target >= candidates[i]; ++i) {
        combination.push_back(candidates[i]);
        backtrack(res, candidates, combination, target - candidates[i], i);
        combination.pop_back();
    }
}

vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
    vector<vector<int>> res;
    vector<int> combination;
    backtrack(res, candidates, combination, target, 0);
    return res;
}

int main() {
    vector<int> candidates = {2, 3, 6, 7};
    int target = 7;
    vector<vector<int>> result = combinationSum(candidates, target);

    cout << "All combinations that sum up to " << target << " are:\n";
    for (const auto& comb : result) {
        cout << "[";
        for (int num : comb) {
            cout << num << " ";
        }
        cout << "]\n";
    }

    return 0;
}
```

This code defines a function `combinationSum` which takes a vector of candidate numbers `candidates` and a target sum `target`, and returns a vector of vectors containing all unique combinations of numbers from `candidates` that sum up to `target`.

The `backtrack` function recursively explores all possible combinations starting from a given index `start`. If the current combination sums up to the target, it's added to the result. Otherwise, it tries adding each candidate number (starting from `start`) to the current combination and recurses to find combinations that sum up to the remaining target.

In the `main` function, we initialize a vector of candidates and a target value, then call the `combinationSum` function to find all combinations that sum up to the target, and finally, we print out the result.

### 1. Algorithms & Data Structures (C++): Find Permutation

Sure, finding permutations in C++ can be done using both recursive and iterative approaches. Here's a recursive approach using backtracking:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void permute(vector<int>& nums, int start, vector<vector<int>>& result) {
    if (start == nums.size() - 1) {
        result.push_back(nums);
        return;
    }
    for (int i = start; i < nums.size(); ++i) {
        swap(nums[start], nums[i]);
        permute(nums, start + 1, result);
        swap(nums[start], nums[i]); // backtracking
    }
}

vector<vector<int>> findPermutations(vector<int>& nums) {
    vector<vector<int>> result;
    permute(nums, 0, result);
    return result;
}

int main() {
    vector<int> nums = {1, 2, 3};
    vector<vector<int>> permutations = findPermutations(nums);
    
    for (const auto& perm : permutations) {
        for (int num : perm) {
            cout << num << " ";
        }
        cout << endl;
    }
    
    return 0;
}
```

This code will output all permutations of the given vector `nums`. You can change the `nums` vector to any other sequence of numbers to find permutations of that sequence.

This code utilizes backtracking technique to generate all possible permutations of the input array. The function `permute` recursively generates permutations by swapping elements in the array and backtracking.

### 1. Algorithms & Data Structures (C++): Knight on chess Board

Implementing a solution for the Knight's Tour problem in C++ involves using backtracking to find a sequence of moves for a knight to cover all squares of a chessboard exactly once. Here's a basic implementation:

```cpp
#include <iostream>
#include <vector>
using namespace std;

const int N = 8; // Size of the chessboard

// Utility function to check if a given cell (x, y) is valid
bool isSafe(int x, int y, vector<vector<int>>& board) {
    return (x >= 0 && y >= 0 && x < N && y < N && board[x][y] == -1);
}

// Utility function to print the solution
void printSolution(vector<vector<int>>& board) {
    for (int i = 0; i < N; ++i) {
        for (int j = 0; j < N; ++j) {
            cout << board[i][j] << "\t";
        }
        cout << endl;
    }
}

// Recursive function to solve Knight's tour problem
bool solveKTUtil(int x, int y, int movei, vector<vector<int>>& board, int xMove[], int yMove[]) {
    int next_x, next_y;
    if (movei == N * N)
        return true;

    // Try all next moves from the current coordinate x, y
    for (int k = 0; k < 8; ++k) {
        next_x = x + xMove[k];
        next_y = y + yMove[k];
        if (isSafe(next_x, next_y, board)) {
            board[next_x][next_y] = movei;
            if (solveKTUtil(next_x, next_y, movei + 1, board, xMove, yMove))
                return true;
            else
                board[next_x][next_y] = -1; // Backtrack
        }
    }
    return false;
}

// Main function to solve Knight's tour problem
bool solveKT() {
    vector<vector<int>> board(N, vector<int>(N, -1));

    // Possible moves for a knight
    int xMove[8] = {2, 1, -1, -2, -2, -1, 1, 2};
    int yMove[8] = {1, 2, 2, 1, -1, -2, -2, -1};

    // Start from the top-left corner
    board[0][0] = 0;

    // Call the recursive function
    if (!solveKTUtil(0, 0, 1, board, xMove, yMove)) {
        cout << "Solution does not exist";
        return false;
    } else {
        cout << "Solution:\n";
        printSolution(board);
    }
    return true;
}

int main() {
    solveKT();
    return 0;
}
```

This code finds a Knight's Tour on an 8x8 chessboard. You can adjust the `N` constant to change the size of the chessboard.

### 1. Algorithms & Data Structures (C++): Letter Combinations of a Phone Number

To generate all possible letter combinations of a phone number in C++, you can use backtracking. Here's a sample implementation:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

// Map to convert digits to corresponding letters
const vector<string> digitToLetters = {
    "",     // 0
    "",     // 1
    "abc",  // 2
    "def",  // 3
    "ghi",  // 4
    "jkl",  // 5
    "mno",  // 6
    "pqrs", // 7
    "tuv",  // 8
    "wxyz"  // 9
};

// Backtracking function to generate combinations
void generateCombinations(const string& digits, int index, string& current, vector<string>& result) {
    // Base case: if current combination is complete, add it to the result
    if (index == digits.size()) {
        result.push_back(current);
        return;
    }

    // Get letters corresponding to the current digit
    string letters = digitToLetters[digits[index] - '0'];

    // Iterate over each letter and append it to the current combination
    for (char letter : letters) {
        current.push_back(letter);
        // Recur with next digit
        generateCombinations(digits, index + 1, current, result);
        // Backtrack: remove the last letter to try a different one
        current.pop_back();
    }
}

// Function to generate letter combinations
vector<string> letterCombinations(const string& digits) {
    vector<string> result;
    if (digits.empty()) return result;
    string current;
    generateCombinations(digits, 0, current, result);
    return result;
}

// Example usage
int main() {
    string digits = "23"; // Example phone number
    vector<string> combinations = letterCombinations(digits);
    // Print the combinations
    for (const string& combination : combinations) {
        cout << combination << endl;
    }
    return 0;
}
```

This code defines a function `letterCombinations` that takes a string of digits representing a phone number and returns a vector of strings containing all possible letter combinations. The `generateCombinations` function is a recursive backtracking function that generates all combinations of letters for the given digits.

### 1. Algorithms & Data Structures (C++): The Recursive Backtracking Portion

Recursive backtracking is a powerful technique used in algorithms and data structures to solve problems that involve making a sequence of decisions. It involves solving problems incrementally by trying out different combinations or possibilities, backtracking when necessary, and exploring alternative solutions until a satisfactory outcome is reached. In C++, you can implement recursive backtracking using functions that call themselves to explore different paths.

Here's a basic overview of how recursive backtracking works in C++, along with an example implementation of solving the N-Queens problem:

1. **Define the Problem**: Clearly define the problem you want to solve and identify the decision points and constraints involved.

2. **Design the Recursive Function**: Create a recursive function that explores all possible solutions by making decisions and recursively exploring further paths. The function should return when a solution is found or when it determines that no solution is possible.

3. **Base Case**: Define the base case(s) that indicate when to stop recursion. Typically, this is when a solution is found or when no further progress can be made.

4. **Recursive Case**: Define the recursive case(s) where the function calls itself to explore further possibilities. Ensure that you properly backtrack when necessary.

5. **Backtracking**: When a dead-end is reached (i.e., no valid solution can be found), backtrack to the previous decision point and explore alternative paths.

6. **Implement Constraints**: Ensure that the recursive function respects any constraints of the problem to avoid exploring invalid paths unnecessarily.

Here's a simple example of solving the N-Queens problem using recursive backtracking in C++:

```cpp
#include <iostream>
#include <vector>

using namespace std;

bool isSafe(const vector<int>& board, int row, int col) {
    // Check if the current position is attacked by any queen in previous rows
    for (int i = 0; i < row; ++i) {
        if (board[i] == col || abs(i - row) == abs(board[i] - col))
            return false; // Same column or same diagonal
    }
    return true;
}

void solveNQueensUtil(vector<int>& board, int row, vector<vector<int>>& solutions) {
    int n = board.size();
    if (row == n) {
        // Base case: All queens are placed successfully
        solutions.push_back(board);
        return;
    }

    for (int col = 0; col < n; ++col) {
        if (isSafe(board, row, col)) {
            board[row] = col; // Place queen at this position
            solveNQueensUtil(board, row + 1, solutions); // Recursive call
            board[row] = -1; // Backtrack
        }
    }
}

vector<vector<int>> solveNQueens(int n) {
    vector<vector<int>> solutions;
    vector<int> board(n, -1); // Initialize the board with -1 (no queen placed)
    solveNQueensUtil(board, 0, solutions);
    return solutions;
}

int main() {
    int n = 4;
    vector<vector<int>> solutions = solveNQueens(n);
    for (const auto& solution : solutions) {
        for (int row = 0; row < n; ++row) {
            for (int col = 0; col < n; ++col) {
                if (solution[row] == col)
                    cout << "Q ";
                else
                    cout << ". ";
            }
            cout << endl;
        }
        cout << endl;
    }
    return 0;
}
```

This code solves the classic N-Queens problem using recursive backtracking. The `isSafe` function checks whether it's safe to place a queen in the current position, and the `solveNQueensUtil` function recursively explores all possible solutions. Finally, the `solveNQueens` function initializes the board and starts the recursion.

Understanding recursive backtracking takes practice, as it involves thinking recursively and considering all possible paths through the problem space. However, once mastered, it's a versatile technique for solving a wide range of problems efficiently.

### 1. Algorithms & Data Structures (C++): Uber Backtracking question: Combination Sum

Combination Sum is a classic backtracking problem that asks for all unique combinations of candidates that sum up to a given target. For instance, given candidates `[2, 3, 6, 7]` and target `7`, the solution would be `[[2, 2, 3], [7]]`, as 2 + 2 + 3 = 7 and 7 = 7.

Here's a C++ implementation using backtracking:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

void backtrack(vector<vector<int>>& result, vector<int>& candidates, vector<int>& combination, int target, int start) {
    if (target < 0) return; // If target goes negative, it's not a valid combination
    if (target == 0) {
        result.push_back(combination); // If target is reached, add the combination to the result
        return;
    }
    for (int i = start; i < candidates.size(); ++i) {
        combination.push_back(candidates[i]); // Choose
        backtrack(result, candidates, combination, target - candidates[i], i); // Explore
        combination.pop_back(); // Un-choose
    }
}

vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
    vector<vector<int>> result;
    vector<int> combination;
    sort(candidates.begin(), candidates.end()); // Sort candidates to handle duplicates
    backtrack(result, candidates, combination, target, 0);
    return result;
}

int main() {
    vector<int> candidates = {2, 3, 6, 7};
    int target = 7;
    vector<vector<int>> result = combinationSum(candidates, target);
    cout << "Unique combinations that sum up to " << target << ":" << endl;
    for (const auto& combination : result) {
        cout << "[";
        for (int i = 0; i < combination.size(); ++i) {
            cout << combination[i];
            if (i < combination.size() - 1) cout << ", ";
        }
        cout << "]" << endl;
    }
    return 0;
}
```

This code sorts the candidates to handle duplicates properly and calls the `backtrack` function to explore all possible combinations. It starts with an empty combination and tries adding candidates to it recursively until the target is reached or exceeded. If the target is reached, the combination is added to the result.

### 1. Algorithms & Data Structures (C++): What is backtracking

Backtracking is a fundamental technique used in algorithms to systematically search for solutions to problems, especially in scenarios where exhaustive search is impractical. It is often employed in problems involving combinatorial optimization, constraint satisfaction, and decision-making.

In backtracking, you start with an empty solution and incrementally build it up, exploring different possibilities at each step. If you reach a point where you cannot proceed further because of a constraint violation or because all possibilities have been exhausted, you backtrack to the previous decision point and try a different path.

Here's a simplified outline of how backtracking works:

1. **Decision**: Make a decision to add an element to the solution.
2. **Check**: Check if the decision violates any constraints.
3. **Base Case**: If the solution is complete (all constraints are satisfied), return the solution.
4. **Recursion**: Recur to solve the subproblem with the decision added to the solution.
5. **Backtrack**: If the recursion does not lead to a valid solution, backtrack by undoing the decision and try another alternative.

Backtracking is often implemented using recursion, where each recursive call represents a decision point, and backtracking occurs implicitly as the function calls return. It effectively traverses a tree of potential solutions, pruning branches that cannot lead to a valid solution.

Common examples of problems solved using backtracking include the N-Queens problem, Sudoku, and the subset sum problem. In C++, you can implement backtracking algorithms using recursion and possibly additional data structures to store intermediate states.

### 1. Algorithms & Data Structures (C++): What is Backtracking?

Backtracking is a problem-solving technique used in algorithm design. It is especially useful for problems that involve finding all possible solutions to a combinatorial problem. The basic idea behind backtracking is to systematically explore all potential candidates for a solution by trying each candidate and recursively exploring further if the candidate leads to a valid solution or undoing the previous steps if it does not.

In backtracking, you move forward with a partial solution, trying to extend it until you reach a valid solution or find that it is impossible to continue. If you cannot continue, you backtrack to the previous decision point and try a different path. This process continues until all possible solutions are found or until a solution is found that satisfies the problem constraints.

Backtracking is typically implemented using recursion, where each recursive call represents a decision point in the search space. The key components of a backtracking algorithm include:

1. **Decision**: At each step, you make a decision on how to proceed based on the current partial solution.
2. **Feasibility Check**: You check whether the current partial solution satisfies the problem constraints.
3. **Solution Check**: You check if the current partial solution is a valid solution to the problem.
4. **Backtrack**: If the current partial solution cannot be extended further or does not lead to a valid solution, you undo the last decision and backtrack to the previous decision point to explore other possibilities.

Backtracking is commonly used to solve problems such as permutation, combination, subset, and maze problems. It is a fundamental technique used in many algorithmic problems where exhaustive search is required.

### 1. Algorithms & Data Structures (C++): Amazon Backtracking question: Letter Combination of a Phone Number

Sure, the "Letter Combinations of a Phone Number" problem is a classic backtracking problem. Here's the problem statement and a possible solution in C++:

**Problem Statement:**

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![Phone Number to Letters Mapping](https://leetcode.com/problems/letter-combinations-of-a-phone-number/Figures/17/17_telephone_keypad.png)

**Example:**

Input: "23"

Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]

**Solution in C++:**

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

class Solution {
public:
    vector<string> letterCombinations(string digits) {
        if (digits.empty()) return {};
        
        vector<string> result;
        string combination;
        backtrack(digits, 0, combination, result);
        return result;
    }
    
    void backtrack(const string& digits, int index, string& combination, vector<string>& result) {
        // Base case: if the combination is of full length, add it to the result.
        if (index == digits.length()) {
            result.push_back(combination);
            return;
        }
        
        // Mapping of digits to letters
        const vector<string> letters = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
        
        // Get the current digit
        char digit = digits[index];
        // Get the corresponding letters for the current digit
        string possibleLetters = letters[digit - '0'];
        
        // Iterate through each letter and backtrack
        for (char letter : possibleLetters) {
            combination.push_back(letter); // Choose
            backtrack(digits, index + 1, combination, result); // Explore
            combination.pop_back(); // Un-choose
        }
    }
};

int main() {
    Solution sol;
    string input = "23";
    vector<string> result = sol.letterCombinations(input);
    cout << "Letter Combinations: ";
    for (const string& comb : result) {
        cout << comb << " ";
    }
    cout << endl;
    return 0;
}
```

This solution utilizes backtracking to generate all possible combinations of letters corresponding to the given digits. We start with an empty combination and iterate through each digit of the input string. For each digit, we retrieve the corresponding letters and recursively explore all possible combinations. Once we reach the end of the input string, we add the combination to the result.
