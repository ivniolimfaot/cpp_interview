# Templates

## General Info

### What is a template class and template function?

Before talking about templates, we should talk about the idea of *Generics in C++*.

Generics is the idea to allow type (built-in types and user-defined types) to be a parameter to methods, classes and interfaces. For example, classes like an array, map, etc, which can be used using generics very efficiently. We can use them for any type. The method of Generic Programming is implemented to increase the efficiency of the code. Generic Programming enables the programmer to write a general algorithm which will work with all data types. It eliminates the need to create different algorithms if the data type is an integer, string or a character. The advantages of Generic Programming are

1. Code Reusability
1. Avoid Function Overloading
1. Once written it can be used for multiple times and cases.

Generics can be implemented in C++ using *Templates*.

***Templates*** are a feature of the C++ programming language that allows functions and classes to operate with generic types. This allows a function or class declaration to reference via a generic variable another different class without creating full declaration for each of these different classes.

In plain terms, a templated class or function would be the equivalent of (before "compiling") copying and pasting the templated block of code where it is used, and then replacing the template parameter with the actual one. For this reason, classes employing templated methods place the implementation in the headers (*.h files) as no symbol could be compiled without knowing the type beforehand.

The C++ Standard Library provides many useful functions within a framework of connected templates.

#### Function templates

A function template behaves like a function except that the template can have arguments of many different types. In other words, a function template represents a family of functions. A function template starts with the keyword ``template`` followed by template parameter(s) inside ``<>`` which is followed by the function definition:

```cpp
template <typename T>
T functionName(T parameter1, T parameter2, ...) {
    // code
}
```

In the above code, **T** is a template argument that accepts different data types (int, float, etc.), and ``typename`` is a ***keyword***. When an argument of a data type is passed to *functionName()*, the compiler generates a new version of *functionName()* for the given data type.

Once we've declared and defined a function template, we can call it in other functions or templates with the following syntax:

```cpp
int main() {

    int result1;
    double result2;
    // calling with int parameters
    result1 = functionName<int>(2, 3);
    cout << result1 << endl;

    // calling with double parameters
    result2 = functionName<double>(2.2, 3.3);
    cout << result2 << endl;

    return 0;
}    
```

#### Class tempplates

Similar to function templates, we can use class templates to create a single class to work with different data types. Class templates come in handy as they can make our code shorter and more manageable.

A class template starts with the keyword ``template`` followed by template parameter(s) inside ``<>`` which is followed by the class declaration.

```cpp
template <class T>
class className {
  private:
    T var;
    ... .. ...
  public:
    T functionName(T arg);
    ... .. ...
};
```

In the above declaration, **T** is the template argument which is a placeholder for the data type used, and class is a ***keyword***. Inside the class body, a member variable *var* and a member function *functionName()* are both of type **T**.

Once we've declared and defined a class template, we can create its objects in other classes or functions with the following syntax:

```cpp
className<dataType> classObject;
```

***For example,***

```cpp
className<int> classObject;
className<float> classObject;
className<string> classObject;
```

##### Defining a Class Member Outside the Class Template

Suppose we need to define a function outside of the class template. We can do this with the following code:

```cpp
template <class T>
class ClassName {
    ... .. ...
    // Function prototype
    returnType functionName();
};

// Function definition
template <class T>
returnType ClassName<T>::functionName() {
    // code
}
```

The code template ``<class T>`` is repeated while defining the function outside of the class. This is necessary and is part of the syntax.

##### C++ Class Templates With Multiple Parameters

We can use multiple template parameters and even use default arguments for those parameters. For example,

```cpp
template <class T, class U, class V = int>
class ClassName {
  private:
    T member1;
    U member2;
    V member3;
    ... .. ...
};
```

### The instantiation of a template

***Template instantiation*** is the process of generating specific code from a template when it is used with particular template arguments.
When a template is instantiated with specific template arguments, the compiler generates the code for the template with those arguments, creating concrete functions or classes. Template instantiation happens automatically by the compiler when the template is used in the code.

```cpp
template<typename T>
void foo(T arg) {
    // code
}

int main() {
    foo<int>(5); // Instantiates foo<int>
    foo<double>(3.14); // Instantiates foo<double>
    return 0;
}
```

#### Implicit and Exlicit instantiation

Template instantiation can occur either implicitly or explicitly.

***Implicit Template Instantiation***

Implicit template instantiation occurs when the compiler generates the code for a template automatically, without explicit direction from the programmer. This happens when the compiler encounters a usage of the template in the code, and it needs to generate the specific code for that template with the provided template arguments. Implicit instantiation is the default behavior for templates in most cases.

```cpp
template<typename T>
void foo(T arg) {
    // code
}

int main() {
    foo<int>(5); // Implicit instantiation for foo<int>
    foo<double>(3.14); // Implicit instantiation for foo<double>
    return 0;
}
```

***Explicit Template Instantiation***

Explicit template instantiation occurs when the programmer explicitly tells the compiler to generate the code for a template with specific template arguments. This is done using the template keyword followed by the declaration or definition of the template with the desired template arguments. Explicit instantiation can be useful for reducing compilation times, especially in large projects where templates are heavily used.

```cpp
template<typename T>
void bar(T arg) {
    // code
}

template void bar<int>(int); // Explicit instantiation for bar<int>

int main() {
    bar<double>(3.14); // Implicit instantiation for bar<double>
    return 0;
}
```

### What is template specialization? Partial specialization of a template?

**Template specialization** in C++ allows to provide a specific implementation of a template for a particular data type or set of data types. This is useful when the default behavior of the template is not suitable for certain types, or when you want to optimize the code for specific types. There are two types of template specialization in C++: explicit specialization and partial specialization.

***Explicit specialization***

In explicit specialization, you provide a specialized implementation of the entire template for a specific data type. This is typically used when the default template implementation is not appropriate for the specialized type.

```cpp
// Generic template
template<typename T>
class MyClass {
public:
    void print() {
        std::cout << "Generic template" << std::endl;
    }
};

// Explicit specialization for int
template<>
class MyClass<int> {
public:
    void print() {
        std::cout << "Specialized template for int" << std::endl;
    }
};
```

***Partial specialization***

In partial specialization, you provide a specialized implementation for a subset of the template parameters. This is commonly used with class templates, where you may want to specialize based on multiple template parameters.

```cpp
// primary class
template <typename T>
class Vector
{ /* ... implementation of a container class for objects of type T... */ };

// partial specialization of the primary class for storing pointers

template <typename T>
class Vector<T*>
{ /* ... implementation of a container class for pointers to objects of type T... */ };
```

### Tell me about the implementation of template classes in a cpp file?

To implement a template class in a `.cpp` file in C++, you typically need to include both the template declaration and definition in the same file. Here's an example demonstrating how to implement a template class in a `.cpp` file:

```cpp
// TemplateClass.h (Header file)

#ifndef TEMPLATECLASS_H
#define TEMPLATECLASS_H

template <typename T>
class TemplateClass {
public:
    TemplateClass(T value);
    void setValue(T value);
    T getValue() const;

private:
    T m_value;
};

#include "TemplateClass.cpp" // Include the implementation file here

#endif
```

```cpp
// TemplateClass.cpp (Implementation file)

#include "TemplateClass.h"

template <typename T>
TemplateClass<T>::TemplateClass(T value) : m_value(value) {}

template <typename T>
void TemplateClass<T>::setValue(T value) {
    m_value = value;
}

template <typename T>
T TemplateClass<T>::getValue() const {
    return m_value;
}
```

In this example, `TemplateClass.h` declares the template class `TemplateClass`, and the implementation is provided in `TemplateClass.cpp`. Make sure to include the implementation file at the end of the header file, so the compiler can see the implementation of the template class when instantiating it.

Remember that when you use a template class, the compiler needs to see both the declaration and definition at the point of instantiation. Therefore, including the `.cpp` file at the end of the header file allows the compiler to see both when you include the header file in other source files.

### What are the rules of type deduction in a template?

In C++, template type deduction is the process by which the compiler determines the template argument types based on the types of the function arguments passed to the template function or class. There are specific rules that govern how type deduction occurs:

1. **Function Template Type Deduction**:
   - When a function template is called, the compiler deduces the template arguments from the function arguments.
   - The compiler uses the function arguments to deduce the template argument types.
   - If there are multiple arguments, the types are deduced independently from each argument.
   - Deduction does not consider implicit conversions unless necessary.

2. **Template Argument Deduction for Class Templates**:
   - For class templates, deduction often happens from constructor arguments.
   - Template argument deduction happens during class template instantiation.
   - The compiler deduces template arguments from the constructor arguments when you create an object of the class template.

3. **Deduction Failure**:
   - Deduction can fail if the compiler cannot deduce the template argument types.
   - This can happen due to ambiguous function calls or when the function call does not match any template.
   - In such cases, you might need to provide explicit template arguments.

4. **Reference Collapsing Rules**:
   - When deducing types involving references, reference collapsing rules apply.
   - These rules define how references in type deduction are handled, particularly when dealing with reference-to-reference situations.

5. **Array and Function Arguments**:
   - Array-to-pointer decay happens during type deduction. When arrays are passed as function arguments, they decay into pointers.
   - Function types decay into pointers to functions during deduction.

6. **Template Argument Deduction with Auto**:
   - C++11 introduced the `auto` keyword, which allows automatic type deduction.
   - `auto` can be used in conjunction with templates to simplify syntax, as the compiler deduces the type based on the initializer expression.

7. **Non-Deduced Contexts**:
   - Certain contexts prevent type deduction, such as non-deduced contexts.
   - Examples include the use of type conversion functions, member access in templates, etc.

Understanding these rules is crucial for effectively using templates in C++ and ensuring that type deduction occurs correctly. Incorrect deduction can lead to compilation errors or unexpected behavior.

Sure, let's go through some examples to illustrate the rules of type deduction in C++ templates:

1. **Function Template Type Deduction**:

```cpp
template<typename T>
void printType(T arg) {
    std::cout << typeid(arg).name() << std::endl;
}

int main() {
    printType(5);  // Deduces T as int
    printType(3.14);  // Deduces T as double
    printType("Hello");  // Deduces T as const char*
    return 0;
}
```

1. **Template Argument Deduction for Class Templates**:

```cpp
template<typename T>
class MyContainer {
public:
    MyContainer(T value) : data(value) {}
    void print() { std::cout << data << std::endl; }
private:
    T data;
};

int main() {
    MyContainer<int> container1(10);  // T is int
    container1.print();

    MyContainer<double> container2(3.14);  // T is double
    container2.print();

    return 0;
}
```

1. **Reference Collapsing Rules**:

```cpp
template<typename T>
void foo(T&& arg) {
    // Deduces T, reference collapsing rules apply
    // T is int& if arg is an lvalue, T is int if arg is an rvalue
}

int main() {
    int x = 5;
    foo(x);  // T is int&
    foo(10); // T is int
    return 0;
}
```

1. **Template Argument Deduction with Auto**:

```cpp
template<typename T>
void printType(T arg) {
    std::cout << typeid(arg).name() << std::endl;
}

int main() {
    auto x = 5;
    printType(x);  // Deduces T as int
    auto y = 3.14;
    printType(y);  // Deduces T as double
    auto z = "Hello";
    printType(z);  // Deduces T as const char*
    return 0;
}
```

These examples demonstrate various scenarios of template type deduction in C++, including function templates, class templates, reference collapsing rules, and the use of `auto` for type deduction.

### 97. What is the difference between using and typedef?

In C++, both `using` and `typedef` are used to create aliases for existing data types, but they have some differences:

1. **Syntax**:

   - `typedef` is older and its syntax is a bit different:

     ```cpp
     typedef existing_type new_name;
     ```

   - `using` is more modern and has a cleaner syntax:

     ```cpp
     using new_name = existing_type;
     ```

2. **Usage**:

   - `typedef` can only be used to create aliases for types, such as fundamental types (like `int`, `float`, etc.), custom types (like structs, unions, enums), and pointers.
   - `using` can be used to create aliases for types as well as templates, function pointers, and function types.

3. **Scope**:

   - `typedef` defines a new name within the current scope.
   - `using` allows you to declare an alias within a narrower scope using the block scope syntax `{}`, providing finer control over the visibility of the alias.

4. **Ease of Understanding**:

   - `using` is generally considered easier to read and understand, especially for more complex declarations involving templates.

Here's an example demonstrating the usage of both:

```cpp
// typedef
typedef int Int32;
typedef void (*FunctionPtr)(int);

// using
using Int32 = int;
using FunctionPtr = void (*)(int);
```

Both of the above declarations create an alias for `int` called `Int32` and an alias for a function pointer that takes an `int` argument and returns `void` called `FunctionPtr`.

### 98. How much memory does an random structure take? What is the object alignment?

The memory usage of a random structure in C++ depends on several factors, including the size and alignment requirements of its members, padding added by the compiler for alignment, and any additional overhead for bookkeeping purposes.

Let's consider a simple example of a structure with a few member variables:

```cpp
#include <iostream>

struct RandomStruct {
    int a;
    char b;
    double c;
};

int main() {
    std::cout << "Size of RandomStruct: " << sizeof(RandomStruct) << " bytes" << std::endl;
    return 0;
}
```

In this example, `RandomStruct` contains an integer (`int`), a character (`char`), and a double-precision floating-point number (`double`). To find out how much memory this structure occupies, we can use the `sizeof` operator in C++. The `sizeof` operator returns the size of its operand in bytes.

The actual size of `RandomStruct` may not be simply the sum of the sizes of its members due to padding added by the compiler for alignment purposes. Padding is added to ensure that each member of the structure is properly aligned in memory, which can improve performance.

To get an accurate measurement of the memory usage, you can use the `sizeof` operator as shown in the example above. This will give you the size of the structure in bytes. Keep in mind that the size might vary depending on the compiler and the platform you're using.

Object alignment refers to the memory allocation strategy used by compilers to ensure that data is stored in memory at addresses that are multiples of a particular value, known as the alignment requirement.

Alignment is important for efficient memory access, especially on architectures where unaligned memory access can be slower or even unsupported. Most modern processors have specific alignment requirements for different data types. For example, many processors require that 4-byte integers (`int`) be aligned to addresses that are multiples of 4 bytes, and 8-byte doubles (`double`) be aligned to addresses that are multiples of 8 bytes.

Compilers typically handle alignment automatically, adding padding between structure members if necessary to ensure proper alignment. This padding ensures that each member of a structure is stored at an address that meets the alignment requirements of its data type. Padding can increase the memory usage of a structure, but it improves memory access efficiency, which can lead to better performance.

In C and C++, you can control alignment explicitly using compiler-specific directives or attributes, such as `alignas` in C++11 and later or `__attribute__((aligned))` in GCC. However, in most cases, relying on the compiler's default alignment behavior is sufficient.

### 99. Why does an empty structure take 1 byte? What is the minimum addressing unit in C++?

In C++, an empty structure still occupies memory because every instance of a structure in memory must have a unique address. Even though an empty structure does not contain any data members, it still needs to have a distinct memory address from other objects.

Therefore, the compiler ensures that an empty structure occupies at least one byte of memory to ensure uniqueness of addresses. This is because, in C++, two distinct objects must have distinct addresses. So even though there are no data members, the compiler allocates at least one byte of memory to ensure that each instance of the empty structure has its own unique address.

However, it's worth noting that the actual size of the structure might be larger than 1 byte due to alignment requirements imposed by the compiler. This means the compiler might add padding bytes to ensure that the structure is aligned properly in memory, which is typically done for performance reasons, especially in architectures where accessing misaligned data can be inefficient.

The minimum addressing unit in C++ is typically one byte. This means that memory is typically addressed at the byte level. In other words, the smallest unit of memory that can be individually addressed and manipulated in C++ programs is one byte.

However, it's important to note that the C++ standard doesn't explicitly mandate a specific size for a byte. In most systems, a byte is usually composed of 8 bits, but this is not guaranteed by the C++ standard.

Additionally, C++ provides facilities through its standard library to work with larger data types, such as words (16 bits), double words (32 bits), and quad words (64 bits), but these are usually built on top of the basic byte-level addressing provided by the language.

### 60. What is template specialization?

Template specialization in C++ is a feature that allows you to provide a different implementation of a template for a specific type or set of types. This is useful when the default implementation of a template is not suitable or efficient for certain types. There are two types of template specialization in C++: function template specialization and class template specialization.

#### Function Template Specialization

```cpp
// Primary template
template <typename T>
void foo(T value) {
    // Default implementation
    std::cout << "Generic foo: " << value << std::endl;
}

// Specialization for int type
template <>
void foo<int>(int value) {
    std::cout << "Specialized foo for int: " << value << std::endl;
}
```

In this example, `foo` is a function template. The specialization for `int` type provides a different implementation for `foo` when it's called with an `int` argument.

#### Class Template Specialization

```cpp
// Primary template
template <typename T>
class Bar {
public:
    void print() {
        std::cout << "Generic Bar" << std::endl;
    }
};

// Specialization for double type
template <>
class Bar<double> {
public:
    void print() {
        std::cout << "Specialized Bar for double" << std::endl;
    }
};
```

Here, `Bar` is a class template. The specialization for `double` type provides a different implementation for the `print` method when `Bar` is instantiated with `double`.

#### Notes

1. Template specialization should be used judiciously, as it can lead to code bloat and complexity.
2. Partial specialization is also possible in C++, where only some template parameters are specialized, but it's primarily applicable to class templates.
3. Template specialization can be applied to both function templates and class templates, as shown in the examples above.

Template specialization is a powerful tool in C++ that allows you to customize behavior for specific types while still taking advantage of the generic nature of templates.

### Can a constructor be a template function?

It’s not possible to templatize the destructor as it doesn’t take any parameter and there can be only one destructor in a class - unless you use concepts to constrain them. But it’s totally possible to have a constructor template - even without having a class template.

The syntax is simple. Instead of using the usual template syntax on the class, you apply it to the constructor.

```cpp
class RegularClassWithConstructorTemplate {
public:
  template<typename T>
  RegularClassWithConstructorTemplate(T data) {
    std::cout << "RegularClassWithConstructorTemplate called with " << data << '\n';
  }
private:
};

int main()
{
    // this template constructor could be called like this:
    RegularClassWithConstructorTemplate(56);
}
```

**This constructor can't be called with templated call like this:**

```cpp
  RegularClassWithConstructorTemplate<int>(56);
```

The important difference to keep in mind is that the template type ``T`` **cannot** be used outside the constructor.

### Can a virtual function be a template function?

Yes, a virtual function can indeed be a template function in C++. This allows you to create a base class with a template virtual function and then override that function in derived classes with specific template parameter instantiations.

```cpp
template<typename T>
class Base {
public:
    virtual void foo(T value) {
        std::cout << "Base::foo(" << value << ")" << std::endl;
    }
};

template<typename T>
class Derived : public Base<T> {
public:
    virtual void foo(T value) override {
        std::cout << "Derived::foo(" << value << ")" << std::endl;
    }
};

int main() {
    Base<int>* basePtr = new Derived<int>();
    basePtr->foo(42); // Calls Derived::foo(42)
    delete basePtr;
    return 0;
}
```

``Base`` is a template class with a virtual function *foo()* that is also a template function. The ``Derived`` class then overrides this function with a specific template instantiation. When you call *foo()* through a base class pointer, it calls the overridden function in the derived class.

### What are SFINAE and PIMPL?

SFINAE stands for "Substitution Failure Is Not An Error." It's a principle in C++ template metaprogramming that allows template functions or classes to be enabled or disabled based on whether a particular substitution of template parameters would result in a valid type or expression.

In practical terms, SFINAE allows templates to be more flexible by allowing the compiler to discard certain overloads or specializations from consideration during overload resolution if they would result in an error when instantiated with certain types, rather than causing a hard compilation error.

This principle is commonly used in advanced C++ programming techniques, such as in implementing type traits, enabling/disabling template specializations, and creating more flexible and generic code. It's a powerful tool for creating more expressive and efficient template-based designs in C++.

Simple example to illustrate SFINAE in action:

```cpp
#include <iostream>
#include <type_traits>

// Function template that adds two numbers if both types are arithmetic
template<typename T, typename U,
         typename = std::enable_if_t<std::is_arithmetic_v<T> && std::is_arithmetic_v<U>>>
auto add(T x, U y) -> decltype(x + y) {
    return x + y;
}

int main() {
    std::cout << add(5, 3) << std::endl;   // Should print 8
    //std::cout << add("Hello", "World") << std::endl;   // Compile error, since "Hello" and "World" are not arithmetic types
    return 0;
}
```

In this example:

* We define a function template `add` that takes two parameters of potentially different types.
* We use `std::enable_if` in combination with `std::is_arithmetic` to enable this function only if both types `T` and `U` are arithmetic types.
* If the condition is satisfied, the `decltype(x + y)` syntax ensures that the return type of the function is the same as the result of adding `x` and `y`.
* In the `main` function, we demonstrate calling `add` with two integers, which should work fine. If you uncomment the line that attempts to add two strings, you'll get a compile-time error because the function `add` is not defined for non-arithmetic types. This is an example of SFINAE in action, where the compiler excludes certain overloads from consideration based on the substitution failure.

PIMPL stands for "Pointer to IMPLementation." It is a design pattern used in C++ to hide implementation details of a class from its users. This pattern is also known as the "Opaque Pointer" or "Compiler Firewall" pattern.

In the PIMPL pattern, instead of exposing the details of a class's implementation in its header file, a pointer to an implementation class is used. This allows the implementation details to be hidden from users of the class, reducing compilation dependencies and potentially speeding up compilation times. It also enables better encapsulation and helps to minimize the impact of changes to the implementation on the users of the class.

Here's a basic example of how the PIMPL pattern might be implemented:

```cpp
// Header file (MyClass.h)
class MyClass {
public:
    MyClass();
    ~MyClass();

    void doSomething();

private:
    class MyClassImpl;
    MyClassImpl* pImpl; // Pointer to implementation
};

// Implementation file (MyClass.cpp)
#include "MyClass.h"

class MyClass::MyClassImpl {
public:
    void doSomething() {
        // Implementation details...
    }
};

MyClass::MyClass() : pImpl(new MyClassImpl()) {}

MyClass::~MyClass() {
    delete pImpl;
}

void MyClass::doSomething() {
    pImpl->doSomething();
}
```

In this example, the details of the implementation of `MyClass` are hidden from users of the class. The `MyClassImpl` class is forward-declared in the header file, and its implementation is defined in the source file. This allows changes to the implementation of `MyClass` to be made without requiring users of `MyClass` to recompile their code.

Sure, here are a few examples of situations where the PIMPL pattern can be useful:

1. **Library Interfaces**: When designing a library, you might want to expose only the necessary interface to the users while keeping the implementation details hidden. PIMPL can help achieve this, ensuring that changes to the implementation don't affect the users of the library.

2. **Reducing Compilation Dependencies**: In large codebases, changes to implementation files can trigger recompilation of many other files due to dependencies. By using PIMPL, you can isolate changes to implementation files, reducing the need for recompilation of files that include only the class declaration.

3. **ABI Stability**: When designing a library or interface that's expected to remain stable across different versions or platforms, the PIMPL pattern can help maintain ABI (Application Binary Interface) stability. By hiding implementation details, you can modify the implementation without affecting the ABI as seen by clients of the library.

4. **Dynamic Libraries**: In scenarios where you're working with dynamic libraries (such as DLLs on Windows or shared objects on Unix-based systems), changes to the internal implementation of a class can cause issues if the class is part of the library's public interface. PIMPL allows you to modify the internal implementation without breaking binary compatibility.

5. **Cross-Platform Development**: Different platforms may have different requirements or optimizations for certain operations. With PIMPL, you can have platform-specific implementations hidden behind a common interface, allowing your code to remain portable without exposing platform-specific details.

These examples illustrate how the PIMPL pattern can be beneficial in various software development scenarios, providing encapsulation, modularity, and maintainability benefits.

### 8. What is SFINAE? What is it used for?

SFINAE stands for "Substitution Failure Is Not An Error." It's a principle in C++ template metaprogramming. Essentially, it refers to the behavior where, during the process of template argument deduction, if a substitution of template arguments fails during the instantiation of a template, that particular instantiation isn't considered an error. Instead, the compiler continues trying other overloads or templates.

SFINAE is particularly useful in enabling the selection of template specializations or overloads based on properties of types, like the presence or absence of certain member functions or properties. By allowing certain overloads or specializations to be discarded during overload resolution, it enables more flexible and powerful template programming techniques.

For instance, a common use of SFINAE is in writing template functions or classes that behave differently based on whether certain operations are valid for the types involved. This allows for more generic and adaptable code that can handle a wider variety of types without requiring explicit specialization for each case.

Certainly! Here's a simple example demonstrating the use of SFINAE to select different implementations of a function based on whether a specific member function exists in the input type:

```cpp
#include <iostream>
#include <type_traits>

// Define a test class with and without a specific member function
struct WithFunction {
    void someFunction() {}
};

struct WithoutFunction {};

// Define a function template that only accepts types with a member function 'someFunction'
template<typename T>
typename std::enable_if<std::is_member_function_pointer<decltype(&T::someFunction)>::value>::type
callFunction(const T& obj) {
    std::cout << "Calling someFunction" << std::endl;
    obj.someFunction();
}

// Overload for types that don't have 'someFunction'
template<typename T>
typename std::enable_if<!std::is_member_function_pointer<decltype(&T::someFunction)>::value>::type
callFunction(const T& obj) {
    std::cout << "No someFunction available" << std::endl;
}

int main() {
    WithFunction obj1;
    WithoutFunction obj2;

    callFunction(obj1);  // Calls the version of callFunction for types with 'someFunction'
    callFunction(obj2);  // Calls the version of callFunction for types without 'someFunction'

    return 0;
}
```

In this example, `callFunction` is a function template that takes a parameter of a generic type `T`. Using `std::enable_if`, we enable or disable these function templates based on whether the type `T` has a member function named `someFunction`. If `T` has `someFunction`, the first overload is selected, otherwise, the second overload is selected. This allows the function to behave differently based on the capabilities of the input type, all resolved at compile time using SFINAE.

SFINAE (Substitution Failure Is Not An Error) is primarily used in C++ template metaprogramming to enable or disable function templates or class templates based on properties of types. Here are some common use cases where SFINAE is employed:

1. **Selective Template Specialization**: SFINAE allows you to provide different implementations of a function or class template depending on certain properties of the template arguments, such as the presence or absence of specific member functions, types, or template specializations.

2. **Type Traits**: SFINAE is often used in conjunction with type traits to enable or disable template instantiations based on properties of types at compile time. For example, you can use SFINAE to select different implementations depending on whether a type is arithmetic, a pointer, a class with certain member functions, etc.

3. **Default Behavior Customization**: SFINAE allows you to provide default behavior for templates while still allowing users to customize that behavior by providing their own specializations. The default behavior can be overridden if certain conditions are met, otherwise, the default implementation is used.

4. **Error Handling and Graceful Degradation**: SFINAE can be used to gracefully handle errors or unsupported operations at compile time. Instead of causing a hard compilation error, SFINAE can be leveraged to try alternative function overloads or template specializations that are valid for the given types.

5. **Concepts and Constraints**: With the advent of C++20 concepts, SFINAE is still relevant. Concepts allow for expressing requirements on template arguments more directly, but SFINAE can still be used in scenarios where finer-grained control over template selection is needed or where concepts are not applicable.

In summary, SFINAE is a powerful technique in C++ template metaprogramming that enables more flexible and adaptable code by selectively enabling or disabling template instantiations based on compile-time conditions, ultimately leading to more generic and reusable code.

### 9. What is metaprogramming? How is it implemented in C++?

Metaprogramming is a programming technique where a program is designed to manipulate or generate other programs (or even itself) as its data. In other words, it's writing code that operates on code. Metaprogramming enables developers to create more flexible, dynamic, and efficient software systems by abstracting common patterns, automating repetitive tasks, or enabling customization.

There are several forms of metaprogramming:

1. **Code Generation**: This involves generating code during the compilation or runtime phase based on certain rules or input data. Code generators are often used to produce boilerplate code, such as serialization code or database access layers.

2. **Reflection**: Reflection is the ability of a program to examine and modify its own structure, including classes, methods, and properties, at runtime. This allows for dynamic introspection and modification of code behavior.

3. **Macro Systems**: Macro systems allow programmers to define language extensions or domain-specific languages (DSLs) within a host language. Macros are expanded at compile time, transforming code written in the DSL into standard code in the host language.

4. **Template Metaprogramming**: This technique, commonly used in languages like C++, involves using templates to perform computations at compile time, allowing for code to be generated and optimized based on types and constants known at compile time.

Metaprogramming can lead to more expressive and concise code, but it also comes with challenges such as increased complexity, potential for runtime errors, and reduced readability if not used judiciously.

Metaprogramming in C++ is primarily achieved through two main mechanisms: templates and the preprocessor. Here's a brief overview of each:

1. **Templates**: Templates in C++ are a powerful mechanism for metaprogramming. They allow for the creation of generic code that operates on types rather than specific data values. Template metaprogramming exploits the fact that template instantiation and function overloading resolution occur at compile time. This allows for computations, type transformations, and code generation to be performed during compilation.

   Template metaprogramming techniques often involve using template specialization, constexpr functions, variadic templates, and recursive template instantiation to achieve complex computations and code generation at compile time.

   Here's a simple example of a compile-time computation using templates to calculate the factorial of a number:

   ```cpp
   template <int N>
   struct Factorial {
       static constexpr int value = N * Factorial<N - 1>::value;
   };

   template <>
   struct Factorial<0> {
       static constexpr int value = 1;
   };

   int main() {
       constexpr int result = Factorial<5>::value; // Result calculated at compile time
       return 0;
   }
   ```

2. **Preprocessor Macros**: The C++ preprocessor provides macros, which are directives that are interpreted by the preprocessor and replaced with specified code before compilation. While macros are less powerful and less type-safe compared to templates, they can still be used for simple metaprogramming tasks, such as conditional compilation, code generation, and simple text manipulation.

   However, macros should be used with caution due to their limitations, such as lack of type checking and scoping issues. Here's a simple example of a preprocessor macro for defining a constant:

   ```cpp
   #define MAX(a, b) ((a) > (b) ? (a) : (b))

   int main() {
       int x = 5;
       int y = 10;
       int max_value = MAX(x, y); // Resolved by the preprocessor
       return 0;
   }
   ```

In summary, C++ offers powerful metaprogramming capabilities through templates and preprocessor macros. Templates provide a type-safe and flexible way to perform metaprogramming tasks at compile time, while preprocessor macros offer a simpler, though less robust, mechanism for code generation and manipulation.

### 10. How to use variadic templates?

Variadic templates in C++ are a feature introduced in C++11 that allow functions and classes to accept an arbitrary number of arguments of any type. This feature is particularly useful when you want to create generic code that operates on a variable number of arguments.

Here's a simple example of a variadic template function that sums up its arguments:

```cpp
#include <iostream>

// Base case of the recursion, when there are no more arguments
int sum() {
    return 0;
}

// Recursive case, sums up the first argument and recursively calls itself with the rest of the arguments
template<typename T, typename... Args>
T sum(T first, Args... rest) {
    return first + sum(rest...);
}

int main() {
    std::cout << sum(1, 2, 3, 4, 5) << std::endl; // Output: 15
    std::cout << sum(1.1, 2.2, 3.3) << std::endl; // Output: 6.6
    return 0;
}
```

In this example, `sum()` is a variadic template function. It has two versions: one for the base case (when there are no more arguments), and another for the recursive case. The recursive case takes the first argument and then recursively calls itself with the rest of the arguments until it reaches the base case.

Variadic templates are also commonly used in creating functions like `printf` in C or `std::cout` in C++. They provide a flexible mechanism for dealing with variable numbers of arguments in a type-safe way.

Additionally, variadic templates are not limited to functions; they can also be used to create variadic template classes, allowing for the creation of generic classes that can handle a variable number of template arguments.
