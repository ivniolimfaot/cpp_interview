# Exceptions

## General Info

### What is an exception?

In C++, an exception is an event that disrupts the normal flow of a program's execution. When an exceptional condition occurs during the execution of a program, the program can "throw" an exception. This means it stops its normal execution and transfers control to a special block of code known as an exception handler. The exception handler can then take appropriate actions to deal with the exceptional condition.

Exceptions are typically used to handle errors and other unexpected situations in a program. They provide a mechanism for separating error-handling code from the normal flow of the program, which can improve code readability and maintainability.

In C++, exceptions are typically implemented using the `try`, `catch`, and `throw` keywords:

* `try`: This keyword is used to define a block of code in which exceptions may occur.
* `catch`: This keyword is used to define a block of code that handles exceptions thrown within a `try` block.
* `throw`: This keyword is used to explicitly throw an exception from within a `try` block.

Here's a basic example of how exceptions are used in C++:

```cpp
#include <iostream>

int main() {
    try {
        // Code that may throw an exception
        int x = 10;
        int y = 0;
        if (y == 0) {
            throw std::runtime_error("Division by zero");
        }
        int result = x / y;
        std::cout << "Result: " << result << std::endl;
    } catch (const std::runtime_error& e) {
        // Exception handler
        std::cerr << "Exception caught: " << e.what() << std::endl;
    }
    return 0;
}
```

In this example, if the variable `y` is equal to zero, the program will throw a `std::runtime_error` exception with the message "Division by zero". This exception is then caught by the `catch` block, which prints an error message to the standard error stream.

Exceptions can be used to handle a wide range of error conditions, making them a powerful tool for writing robust and reliable C++ code.


### Under what conditions can an exception be thrown in the constructor?

In C++, exceptions can be thrown in a constructor under various conditions, similar to other functions. Here are some scenarios where exceptions might be thrown in a constructor:

1. **Memory Allocation Failure**: If dynamic memory allocation (`new` operator) fails inside a constructor, it can throw a `std::bad_alloc` exception.

    ```cpp
    class MyClass {
    public:
        MyClass() {
            // Memory allocation
            ptr = new int[1000000000000]; // May throw std::bad_alloc if memory is not available
        }
    
    private:
        int* ptr;
    };
    ```

2. **Constructor of a Member Object Throws**: If a constructor of a member object throws an exception, the exception can propagate to the constructor of the enclosing object.

    ```cpp
    class AnotherClass {
    public:
        AnotherClass() {
            // Constructor throwing an exception
            throw std::runtime_error("Constructor failed");
        }
    };

    class MyClass {
    public:
        MyClass() : anotherObject() {
            // Construction of 'anotherObject' might throw
        }
    
    private:
        AnotherClass anotherObject;
    };
    ```

3. **Invalid Argument**: If the constructor receives invalid arguments, it might throw an exception. This would depend on the specific logic implemented within the constructor to validate inputs.

    ```cpp
    class MyClass {
    public:
        MyClass(int value) {
            if (value < 0) {
                throw std::invalid_argument("Value cannot be negative");
            }
            // other constructor logic
        }
    };
    ```

4. **Resource Acquisition Failure**: If the constructor is involved in acquiring resources like file handles, network connections, etc., and if there's a failure in acquiring those resources, it might throw an exception.

    ```cpp
    class File {
    public:
        File(const std::string& filename) {
            fileHandle = fopen(filename.c_str(), "r");
            if (fileHandle == nullptr) {
                throw std::runtime_error("Failed to open file");
            }
        }
    
        ~File() {
            if (fileHandle != nullptr) {
                fclose(fileHandle);
            }
        }

        // other member functions

    private:
        FILE* fileHandle;
    };
    ```

These are just a few examples. In general, any code inside a constructor that can potentially fail due to exceptional conditions may throw exceptions. It's essential to handle these exceptions properly to maintain program correctness and robustness.


### 52. What does the throw; call do in a catch block?

In C++, when you use `throw;` within a `catch` block, it re-throws the exception that was caught. This means that the same exception is thrown again, allowing outer `try-catch` blocks or the runtime to handle it further up the call stack.

Here's a basic example:

```cpp
#include <iostream>

void someFunction() {
    throw std::runtime_error("Error occurred in someFunction");
}

int main() {
    try {
        someFunction();
    } catch (const std::runtime_error& e) {
        std::cerr << "Caught exception: " << e.what() << std::endl;
        throw; // Re-throwing the caught exception
    }
    return 0;
}
```

In this example, `someFunction()` throws a `std::runtime_error`. In the `catch` block of `main()`, we catch this exception and print out an error message. Then, `throw;` is used to re-throw the same exception, allowing it to propagate further up the call stack or to be caught by an outer `try-catch` block. If there were no `catch` block in `main()` or if `throw;` wasn't used, the program would terminate abruptly.

### 62. What is an exception? How to throw and catch?

In C++, an exception is an object that represents an exceptional condition that arises during the execution of a program. Exceptions are used to handle errors and other exceptional situations in a program in a structured and efficient manner.

Throwing an exception in C++ is done using the `throw` keyword. You can throw any object as an exception, but it's often best practice to throw objects of classes specifically designed for exception handling, such as `std::exception` or its derived classes.

Here's an example of how to throw an exception:

```cpp
#include <iostream>
#include <stdexcept>

void someFunction() {
    // Throw an exception of type std::runtime_error
    throw std::runtime_error("Something went wrong!");
}

int main() {
    try {
        someFunction();
    }
    catch (const std::runtime_error& e) {
        // Catch the exception and handle it
        std::cerr << "Caught an exception: " << e.what() << std::endl;
    }

    return 0;
}
```

In this example:

1. We define a function `someFunction()` which throws a `std::runtime_error` exception.
2. In the `main()` function, we call `someFunction()` inside a try block.
3. If an exception is thrown within `someFunction()`, the control jumps to the catch block where we catch the exception using `catch(const std::runtime_error& e)`.
4. Inside the catch block, we handle the exception. In this case, we simply print an error message using `e.what()` which returns the error message associated with the exception.

Catching an exception in C++ involves using a try-catch block. The syntax is as follows:

```cpp
try {
    // code that may throw an exception
} catch (const SomeExceptionType& e) {
    // code to handle the exception
}
```

The `try` block encloses the code where an exception might be thrown, and the `catch` block catches the exception if it occurs. The exception type specified in the `catch` block should match the type of the exception being thrown or a base class of that exception type.

### 63. What happens if you throw an exception from the constructor? And from the destructor?

Throwing an exception from a constructor in C++ can have significant consequences. When an exception is thrown during the construction of an object, the object's destructor will not be called, and the memory allocated for the object will not be released automatically. This can lead to memory leaks and potential resource leaks if the constructor had acquired any resources.

Furthermore, if the constructor is part of a chain of constructors (e.g., in a derived class), and an exception is thrown from one of the constructors, the destructors for the already constructed base class subobjects will be called to properly clean up those resources.

Here's an example to illustrate:

```cpp
#include <iostream>
using namespace std;

class MyException {};

class MyClass {
public:
    MyClass() {
        cout << "Constructor called." << endl;
        throw MyException(); // throwing an exception from the constructor
    }
    ~MyClass() {
        cout << "Destructor called." << endl;
    }
};

int main() {
    try {
        MyClass obj; // constructor throws exception
    } catch (MyException& e) {
        cout << "Caught exception." << endl;
    }

    return 0;
}
```

In this example, if an exception is thrown from the constructor of `MyClass`, the destructor of `MyClass` will not be called. This can result in resources acquired in the constructor not being properly released, leading to potential memory leaks or other resource leaks.

It's generally considered good practice to handle exceptions within the constructor itself or to ensure that the constructor doesn't throw exceptions by initializing resources safely. If exceptions are thrown from the constructor, it's essential to ensure that any resources acquired are properly cleaned up.

Throwing an exception from a destructor in C++ can also have significant consequences. When an exception is thrown from a destructor, the behavior is generally considered dangerous and should be avoided unless absolutely necessary. Here are some key points to consider:

1. **Termination**: Throwing an exception from a destructor during stack unwinding (due to another exception being thrown) will cause `std::terminate()` to be called, resulting in program termination.

2. **No Handling**: Since destructors are called during the cleanup process when an exception is thrown, there's no reasonable way to handle the exception within the destructor. Throwing exceptions from destructors can lead to cascading failures and make the program's behavior unpredictable.

3. **Resource Leaks**: If an exception is thrown from a destructor, resources may not be properly released. This could lead to memory leaks, file handle leaks, or other resource leaks.

4. **Stack Unwinding**: If an exception is thrown from a destructor while stack unwinding is already in progress due to another exception, it can result in undefined behavior.

Here's a simple example to illustrate the consequences:

```cpp
#include <iostream>
using namespace std;

class MyException {};

class MyClass {
public:
    ~MyClass() {
        cout << "Destructor called." << endl;
        throw MyException(); // throwing an exception from the destructor
    }
};

int main() {
    try {
        MyClass obj; // object created
        throw runtime_error("Some error occurred."); // another exception thrown
    } catch (MyException& e) {
        cout << "Caught exception thrown from destructor." << endl;
    } catch (runtime_error& e) {
        cout << "Caught runtime error: " << e.what() << endl;
    }

    return 0;
}
```

In this example, when an exception is thrown from the destructor of `MyClass`, `std::terminate()` will be called, resulting in program termination. The second exception thrown in the `main()` function will not be caught, leading to undefined behavior.

To avoid such scenarios, it's generally recommended not to throw exceptions from destructors. Instead, ensure that the destructor handles any necessary cleanup operations gracefully without throwing exceptions. If cleanup operations might fail, consider logging errors or using alternative error handling mechanisms.

### 64. What happens if you do not catch an exception?

In C++, if an exception is not caught by any exception handler, it results in the termination of the program. When an exception is thrown and no matching catch block is found to handle it, the program's default behavior is to terminate. This usually results in the program terminating abnormally and may lead to unexpected behavior.

Here's a simple example to illustrate what happens when an exception is not caught:

```cpp
#include <iostream>

void dangerousFunction() {
    throw std::runtime_error("An error occurred!");
}

int main() {
    try {
        dangerousFunction();
    } catch (...) {
        std::cerr << "Caught an exception!" << std::endl;
    }

    std::cout << "Program continues after catching exception." << std::endl;
    return 0;
}
```

If you run this program without the catch block, like this:

```cpp
#include <iostream>

void dangerousFunction() {
    throw std::runtime_error("An error occurred!");
}

int main() {
    dangerousFunction();

    std::cout << "Program continues after catching exception." << std::endl;
    return 0;
}
```

And an exception is thrown from `dangerousFunction()` but not caught, the program will terminate abruptly, and any code after the point where the exception was thrown will not execute. Depending on the operating system and the development environment, you may get an error message indicating the reason for the abnormal termination, such as a segmentation fault or an unhandled exception message.

### 65. What happens if the exception goes beyond the noexcept block of the function?

In C++, if an exception is thrown from within a `noexcept` function, and the function doesn't handle the exception within its own scope, the program will terminate immediately, invoking `std::terminate()`.

Here's an example to illustrate this:

```cpp
#include <iostream>

void noexceptFunction() noexcept {
    throw std::runtime_error("Error occurred inside noexcept function.");
}

int main() {
    try {
        noexceptFunction();
    } catch (const std::exception& e) {
        std::cerr << "Caught exception: " << e.what() << std::endl;
    }

    return 0;
}
```

In this example, the `noexceptFunction()` is declared with `noexcept`, but it still throws an exception. Since there's no exception handling within the function itself, and there's no surrounding `try-catch` block in the calling code (`main()` in this case), the program will terminate when the exception is thrown, and `std::terminate()` will be called.

It's important to handle exceptions appropriately, especially in `noexcept` functions, to prevent unexpected program termination.


### 73. Why are exceptions used?

Exceptions in C++ are used to handle exceptional conditions or errors that occur during the execution of a program. These exceptional conditions could be anything from runtime errors like division by zero, accessing an invalid memory location, or failing to open a file, to logical errors like invalid input or incorrect program state.

The main reasons for using exceptions in C++ are:

1. **Separation of Concerns**: Exceptions allow you to separate the error-handling code from the normal flow of code. This promotes cleaner code organization, as you can focus on writing the core functionality in the main code and handle error conditions separately.

2. **Error Propagation**: Exceptions provide a mechanism for propagating errors up the call stack. If a function encounters an error condition that it cannot handle locally, it can throw an exception, which can then be caught and handled by an appropriate handler higher up in the call stack.

3. **Robustness**: Exception handling helps in writing robust code by providing a structured way to deal with errors. Instead of relying on error codes or special return values to indicate errors, exceptions allow you to handle errors in a more systematic and reliable manner.

4. **Resource Management**: Exceptions can be used to ensure proper resource cleanup even in the presence of errors. For example, if an exception occurs during file I/O or memory allocation, you can use exception handling to ensure that resources like file handles or allocated memory are properly released before the exception is propagated further.

5. **Failure Recovery**: Exceptions provide a mechanism for recovering from errors and continuing execution in a controlled manner. By catching exceptions at appropriate points in the code, you can take corrective actions or gracefully terminate the program if necessary.

However, it's important to use exceptions judiciously and only for truly exceptional conditions. Using exceptions for normal control flow or to handle expected errors can lead to less readable and less efficient code. Additionally, exceptions may incur some performance overhead, so they should be used in situations where the benefits outweigh the costs.

### 74. What are the try-throw-catch blocks?

In C++, `try`, `throw`, and `catch` blocks are used for exception handling. Here's a brief overview of each:

1. `try`: This block is used to enclose the code that might throw an exception. When an exception occurs within the `try` block, the program looks for a matching `catch` block to handle it.

2. `throw`: This keyword is used to explicitly throw an exception within the `try` block. It allows you to indicate that something exceptional has occurred that should be handled by an appropriate `catch` block.

3. `catch`: This block is used to handle exceptions thrown within the corresponding `try` block. It specifies the type of exception it can catch and the actions to take if that type of exception occurs.

Here's a basic example of how they're used together:

```cpp
#include <iostream>

int main() {
    try {
        // Code that might throw an exception
        int numerator = 10;
        int denominator = 0;
        if (denominator == 0) {
            throw std::runtime_error("Divide by zero exception");
        }
        double result = numerator / denominator;
        std::cout << "Result: " << result << std::endl;
    }
    catch (const std::runtime_error& e) {
        // Catch block to handle the exception
        std::cerr << "Exception caught: " << e.what() << std::endl;
    }
    return 0;
}
```

In this example, if the denominator is zero, a `std::runtime_error` exception is thrown using the `throw` keyword. The `catch` block then catches this exception and handles it appropriately by printing an error message.

### 75. Tell us about the logic of catch blocks

In C++, a `try` block is used to enclose code that may throw an exception, and `catch` blocks are used to handle those exceptions. The basic syntax looks like this:

```cpp
try {
    // code that may throw an exception
} catch (ExceptionType1 e1) {
    // handle exception of type ExceptionType1
} catch (ExceptionType2 e2) {
    // handle exception of type ExceptionType2
} catch (...) {
    // handle any other type of exception
}
```

Here's how it works:

1. The code inside the `try` block is executed.
2. If an exception is thrown within the `try` block, the program immediately jumps to the appropriate `catch` block based on the type of exception thrown.
3. If no matching `catch` block is found for the thrown exception type, the exception propagates up the call stack until it either finds a matching `catch` block or reaches the top-level of the program. If no matching `catch` block is found anywhere in the call stack, the program terminates.
4. If a matching `catch` block is found, the code inside that `catch` block is executed to handle the exception.
5. After the `catch` block is executed, program execution continues after the `try-catch` block.

It's important to note a few things:

* Each `catch` block can handle exceptions of a specific type or a hierarchy of types. If a hierarchy of types is used, it's important to order the `catch` blocks from the most specific to the most general types.
* You can have multiple `catch` blocks for different exception types, allowing you to handle each type of exception differently.
* The ellipsis (`...`) catch block is used to catch any type of exception that hasn't been caught by preceding `catch` blocks. This should generally be used sparingly and as a last resort since it makes it harder to diagnose specific exceptions.
* The exception object (e.g., `e1`, `e2` in the example above) can be used within the `catch` block to obtain information about the exception that was thrown, such as its type, message, or other relevant data.
* You can also re-throw an exception from within a `catch` block using the `throw` keyword, allowing you to handle exceptions at different levels of abstraction within your program.

Here's a simple example to illustrate the use of `try` and `catch`:

```cpp
#include <iostream>

void mightGoWrong() {
    bool error = true;
    if (error) {
        throw std::runtime_error("Something went wrong.");
    }
}

int main() {
    try {
        mightGoWrong();
    } catch (const std::exception& e) {
        std::cerr << "Caught exception: " << e.what() << std::endl;
    }

    return 0;
}
```

In this example, the `mightGoWrong` function throws a `std::runtime_error` exception, which is caught in the `main` function's `try-catch` block. The caught exception's message is printed to `std::cerr`.


### 82. What is an exception?

In C++, an exception is an event that disrupts the normal flow of a program's execution. When an exceptional condition occurs during the execution of a program, the program can "throw" an exception. This means it stops its normal execution and transfers control to a special block of code known as an exception handler. The exception handler can then take appropriate actions to deal with the exceptional condition.

Exceptions are typically used to handle errors and other unexpected situations in a program. They provide a mechanism for separating error-handling code from the normal flow of the program, which can improve code readability and maintainability.

In C++, exceptions are typically implemented using the `try`, `catch`, and `throw` keywords:

* `try`: This keyword is used to define a block of code in which exceptions may occur.
* `catch`: This keyword is used to define a block of code that handles exceptions thrown within a `try` block.
* `throw`: This keyword is used to explicitly throw an exception from within a `try` block.

Here's a basic example of how exceptions are used in C++:

```cpp
#include <iostream>

int main() {
    try {
        // Code that may throw an exception
        int x = 10;
        int y = 0;
        if (y == 0) {
            throw std::runtime_error("Division by zero");
        }
        int result = x / y;
        std::cout << "Result: " << result << std::endl;
    } catch (const std::runtime_error& e) {
        // Exception handler
        std::cerr << "Exception caught: " << e.what() << std::endl;
    }
    return 0;
}
```

In this example, if the variable `y` is equal to zero, the program will throw a `std::runtime_error` exception with the message "Division by zero". This exception is then caught by the `catch` block, which prints an error message to the standard error stream.

Exceptions can be used to handle a wide range of error conditions, making them a powerful tool for writing robust and reliable C++ code.

