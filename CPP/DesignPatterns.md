# Design patterns

## General Info

### What are design patterns and what are they used for?

<-- Return to this -->

### Why do we need patterns? What types of patterns are there?

<--- Return later: Design Patterns --->

### Disadvantages of the Singleton pattern? When is it appropriate?

<--- Return later: Design Patterns --->

### What are the advantages and disadvantages of PIMPL?

<--- Return later: Design Patterns --->

### What is the difference between the pattern factory and the factory method? When to use which one?

<--- Return later: Design Patterns --->

### What is the Observer pattern?

<--- Return later: Design Patterns --->

### How to monitor the state of a program? State machine? The State Pattern?

<--- Return later: Design Patterns --->

### What is the Visitor pattern?

<--- Return later: Design Patterns --->

### What are Singleton, Strategy, Template-Method, Decorator patterns?

<-- Return to this -->

### Name generative, structural and behavioral programming patterns and give examples of their use

<--- Return later: Design Patterns --->

### Tell us about design patterns

<--- Return later: Design Patterns --->

### What is Dependency Injection? Give an example

<--- Return later: Design Patterns --->

### What are the design patterns?

Design patterns are reusable solutions to common problems that arise during software development. They provide a template or guideline for structuring code to achieve certain objectives like flexibility, scalability, or maintainability. Design patterns are not specific to a particular programming language or technology; rather, they are general concepts that can be applied across different contexts.

There are several categories of design patterns, including creational, structural, and behavioral patterns. Here's a brief overview of each:

1. Creational Patterns:
   * **Singleton Pattern**: Ensures that a class has only one instance and provides a global point of access to it.
   * **Factory Method Pattern**: Defines an interface for creating an object, but allows subclasses to alter the type of objects that will be created.
   * **Abstract Factory Pattern**: Provides an interface for creating families of related or dependent objects without specifying their concrete classes.
   * **Builder Pattern**: Separates the construction of a complex object from its representation, allowing the same construction process to create different representations.

2. Structural Patterns:
   * **Adapter Pattern**: Allows objects with incompatible interfaces to collaborate.
   * **Decorator Pattern**: Adds additional functionality to objects dynamically.
   * **Facade Pattern**: Provides a simplified interface to a complex subsystem.
   * **Proxy Pattern**: Provides a surrogate or placeholder for another object to control access to it.

3. Behavioral Patterns:
   * **Observer Pattern**: Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
   * **Strategy Pattern**: Defines a family of algorithms, encapsulates each one, and makes them interchangeable. Strategy lets the algorithm vary independently from clients that use it.
   * **Chain of Responsibility Pattern**: Passes a request along a chain of handlers. Upon receiving a request, each handler decides either to process the request or to pass it to the next handler in the chain.
   * **Template Method Pattern**: Defines the skeleton of an algorithm in the superclass but lets subclasses override specific steps of the algorithm without changing its structure.

These are just a few examples, and there are many more design patterns out there. Knowing when and how to apply them can greatly improve the quality, maintainability, and scalability of software systems. However, it's essential to use patterns judiciously, as applying them unnecessarily can lead to over-engineering.

### Why is it not recommended to use Singleton?

The Singleton pattern is often criticized for several reasons, and while it can be useful in certain situations, it's essential to understand its drawbacks before deciding to use it:

1. **Global State**: Singleton introduces global state into your application, which can make it difficult to reason about and test. Any part of the code can access the Singleton instance, potentially leading to unexpected interactions and dependencies.

2. **Coupling**: Code that depends on a Singleton becomes tightly coupled to it, making it harder to change and maintain. Changing the Singleton implementation or replacing it with a different class can require modifications to all the code that depends on it.

3. **Concurrency Issues**: Singleton implementations can be tricky to get right in multithreaded environments. If not properly synchronized, multiple threads accessing the Singleton instance simultaneously can lead to race conditions and unexpected behavior.

4. **Testing Challenges**: Due to its global state and tight coupling, testing code that depends on a Singleton can be difficult. It may be challenging to isolate and mock the Singleton instance for unit testing, leading to more complex and brittle tests.

5. **Hidden Dependencies**: Code that relies on a Singleton often hides its dependencies, making it harder to understand and maintain. When reviewing or debugging code, it may not be immediately clear that a particular component depends on a Singleton instance.

6. **Violation of Single Responsibility Principle**: Singleton classes often take on multiple responsibilities, such as managing their instance creation, maintaining global state, and potentially performing other tasks. This violates the Single Responsibility Principle, making the class less cohesive and harder to maintain.

7. **Difficulty in Extensibility**: Extending a Singleton can be challenging, as it typically involves modifying the Singleton class itself. This can lead to changes rippling through the codebase, impacting other components and increasing the risk of introducing bugs.

While Singleton can be appropriate in some cases, such as managing access to a shared resource or limiting the number of instances of a particular class, it's essential to carefully consider its implications and alternatives before using it. In many situations, dependency injection or other design patterns may offer better solutions that avoid the drawbacks associated with Singleton.

### Explain dependency injection in C++ and how you would implement it

### What is Singleton Design pattern. Explain with an example how to use Singleton Design pattern to design a class that is Thread safe

Sure, I can provide you with an example of a thread-safe Singleton implementation in C++ using locks to ensure safe access in a multi-threaded environment. We'll use a mutex to synchronize access to the creation of the singleton instance.

Here's an example:

```cpp
#include <iostream>
#include <mutex>

class Singleton {
public:
    // Static member function to access the single instance
    static Singleton& getInstance() {
        // Double-checked locking pattern for thread safety
        if (instancePtr == nullptr) {
            std::lock_guard<std::mutex> lock(mutex); // Locking the critical section
            if (instancePtr == nullptr) {
                instancePtr = new Singleton(); // Creating the instance
            }
        }
        return *instancePtr;
    }

    // Other member functions and variables can be added as needed

    void doSomething() {
        std::cout << "Singleton instance is doing something." << std::endl;
    }

private:
    // Private constructor to prevent instantiation
    Singleton() {
        // Constructor code here
    }

    // Private destructor to prevent deletion
    ~Singleton() {
        // Destructor code here
    }

    // Disable copy constructor and assignment operator
    Singleton(const Singleton&) = delete;
    Singleton& operator=(const Singleton&) = delete;

    static Singleton* instancePtr;
    static std::mutex mutex;
};

// Initialization of static members
Singleton* Singleton::instancePtr = nullptr;
std::mutex Singleton::mutex;

int main() {
    // Access the singleton instance from multiple threads
    // Here, we'll just create two threads accessing the instance
    std::thread t1([](){
        Singleton& singleton = Singleton::getInstance();
        singleton.doSomething();
    });

    std::thread t2([](){
        Singleton& singleton = Singleton::getInstance();
        singleton.doSomething();
    });

    t1.join();
    t2.join();

    return 0;
}
```

In this example:

* We've added a static mutex member to the Singleton class to ensure thread safety during the creation of the instance.
* Inside the `getInstance()` function, we're using a double-checked locking pattern to minimize the overhead of locking in the common case where the instance has already been created.
* The `std::lock_guard` is used to automatically lock and unlock the mutex, ensuring that only one thread can create the instance at a time.
* The rest of the Singleton implementation remains the same as in the previous example.

This thread-safe Singleton implementation ensures that only one instance is created even in a multi-threaded environment, and it provides safe access to that instance across threads.

### Lazy initialization

Lazy initialization is a design pattern used in programming, particularly in object-oriented languages like C++. It's a technique where the creation of an object or the execution of a process is delayed until it is actually needed. This can be useful for optimizing performance or resource usage, especially when dealing with objects or processes that are expensive to create or initialize.

In C++, lazy initialization can be implemented in various ways. One common approach is to use a combination of a boolean flag and a pointer. Here's a simple example:

```cpp
#include <iostream>

class LazyObject {
private:
    bool initialized;
    SomeObject* objPtr;

    // Function to lazily initialize the object
    void lazyInitialize() {
        if (!initialized) {
            objPtr = new SomeObject(); // or any initialization logic
            initialized = true;
        }
    }

public:
    LazyObject() : initialized(false), objPtr(nullptr) {}

    // Function to access the lazily initialized object
    SomeObject* getObject() {
        lazyInitialize();
        return objPtr;
    }

    // Destructor to clean up the object if it was initialized
    ~LazyObject() {
        if (initialized) {
            delete objPtr;
        }
    }
};

int main() {
    LazyObject lazyObj;

    // Access the lazily initialized object
    SomeObject* obj = lazyObj.getObject();

    // Use the object
    obj->doSomething();

    return 0;
}
```

In this example, the `LazyObject` class delays the initialization of its `objPtr` member until the `getObject()` function is called. The `initialized` flag ensures that the object is only initialized once. When the `LazyObject` instance is destroyed, it checks if the object was initialized and deletes it if necessary to avoid memory leaks.

This pattern can be useful in situations where the creation of the object is expensive or when you want to avoid unnecessary initialization until the object is actually needed. However, be cautious with lazy initialization as it can introduce complexity and potential issues, such as thread safety concerns in multi-threaded environments.
