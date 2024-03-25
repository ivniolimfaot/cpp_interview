# Testing

## General Info

### What are unit tests for?

<-- Return to this -->

### What is the difference between unit and integration tests?

<-- Return to this -->

### What is TDD?

<-- Return to this -->

### How to test closed methods?

In C++, testing closed methods (methods that are not exposed to the public interface of a class) typically involves unit testing. Unit testing is the process of testing individual units or components of a software. In the case of closed methods, you'll be testing them within the context of the class they belong to.

Here's a general outline of how you can test closed methods in C++ using unit testing frameworks like Google Test or Catch2:

1. **Include the necessary testing framework headers**: You'll need to include the headers for your chosen testing framework in your test files.

2. **Write test cases**: Create test cases to cover various scenarios and behaviors of your closed methods. Test cases should check that the method behaves as expected under different conditions.

3. **Instantiate the class**: Create an instance of the class that contains the closed methods you want to test. You may need to set up any required dependencies or initialize the class appropriately.

4. **Call the closed methods**: Call the closed methods within your test cases, passing in any required parameters.

5. **Assert expected behavior**: Use assertions provided by the testing framework to verify that the closed methods produce the expected results for the given inputs.

6. **Compile and run the tests**: Compile your test code along with the code being tested and any necessary dependencies. Then, run the tests to ensure that the closed methods behave correctly.

Here's a simple example using Google Test:

```cpp
// myclass.h
#ifndef MYCLASS_H
#define MYCLASS_H

class MyClass {
private:
    int add(int a, int b); // Closed method
public:
    int publicMethod(int a, int b);
};

#endif

// myclass.cpp
#include "myclass.h"

int MyClass::add(int a, int b) {
    return a + b;
}

int MyClass::publicMethod(int a, int b) {
    return add(a, b); // Calls the closed method
}

// myclass_test.cpp
#include <gtest/gtest.h>
#include "myclass.h"

TEST(MyClassTest, Add) {
    MyClass obj;
    ASSERT_EQ(obj.publicMethod(2, 3), 5); // Test the closed method indirectly
}

int main(int argc, char **argv) {
    ::testing::InitGoogleTest(&argc, argv);
    return RUN_ALL_TESTS();
}
```

In this example, `add` is a closed method of the `MyClass` class. We're testing it indirectly through the `publicMethod` function. We write test cases in `myclass_test.cpp` file using Google Test framework.

### How to calculate test coverage? Is it necessary to do it?

Test coverage is a measure used to describe the degree to which the source code of a program is executed when a particular test suite runs. It helps in assessing the effectiveness of your tests and identifying areas of code that may not have been adequately tested. In C++, you can calculate test coverage using various tools, with one of the most popular being `gcov` which is often used in conjunction with `gcc`. Here's a step-by-step guide on how to calculate test coverage in C++ using `gcov`:

1. **Compile your code with coverage flags**: First, you need to compile your C++ code with coverage flags. These flags will insert instrumentation code into your executable, which will allow `gcov` to track which parts of your code are executed.

```bash
g++ -o your_program_name -fprofile-arcs -ftest-coverage your_source_code.cpp
```

1. **Run your test suite**: Execute your test suite against the compiled program. This could be a series of unit tests, integration tests, or any other tests you've written to validate your code.

```bash
./your_program_name
```

1. **Generate coverage data**: After running your tests, `gcov` will generate coverage data files for each source file. These files contain information about which lines of code were executed during the tests.

```bash
gcov your_source_code.cpp
```

This will generate a `your_source_code.cpp.gcov` file containing coverage data.

1. **Analyze coverage data**: Open the generated `.gcov` files to analyze the coverage data. These files will show you which lines of code were executed during the test runs and which ones were not.

```bash
less your_source_code.cpp.gcov
```

1. **Interpret the results**: Analyze the coverage data to identify areas of your code that need more testing. You can focus on increasing coverage in these areas by writing additional tests.

Note: `gcov` provides line coverage by default, but you can also get branch coverage by compiling your code with the `-fbranch-probabilities` flag. Additionally, there are other coverage tools available for C++ such as `lcov` which can provide more detailed and human-readable reports on coverage data.

By following these steps, you can effectively calculate test coverage for your C++ code and ensure that your tests adequately exercise your program's functionality.

Calculating test coverage is not strictly necessary, but it is highly recommended for several reasons:

1. **Quality Assurance**: Test coverage helps ensure that your tests exercise most, if not all, of your codebase. This can improve the quality of your software by identifying untested or under-tested areas where bugs might lurk.

2. **Code Confidence**: Having high test coverage can provide developers and stakeholders with greater confidence in the codebase. It indicates that the code has been thoroughly tested and is less likely to contain undiscovered bugs.

3. **Maintenance**: Test coverage can make code maintenance easier. When you have good test coverage, you can refactor code or make changes more confidently, knowing that your tests will catch regressions.

4. **Identification of Dead Code**: Test coverage can help identify dead or unused code in your application. If certain parts of your codebase have consistently low or zero coverage, it might indicate that those areas are unnecessary or obsolete.

5. **Continuous Improvement**: Monitoring test coverage over time can help teams track their testing efforts and identify areas for improvement. It can guide decisions on where to focus testing efforts in future iterations.

6. **Compliance**: In some industries or projects, achieving a certain level of test coverage may be required for compliance with standards or regulations.

While test coverage is valuable, it's essential to understand its limitations. High test coverage does not guarantee the absence of bugs, as tests might not cover all possible edge cases or scenarios. Additionally, focusing solely on increasing test coverage without considering the quality of tests or the effectiveness of testing strategies may not lead to better software quality.

In summary, while it's not strictly necessary to calculate test coverage, doing so can bring several benefits to software development processes, particularly in terms of quality assurance, code confidence, and maintenance.

### What is Unit test for? How does it differ from Functional Test?

Unit testing is a fundamental practice in software development aimed at verifying the correctness of individual units or components of a software application. A unit test focuses on testing the smallest testable parts of an application, typically individual functions, methods, or classes, in isolation from the rest of the system. The primary purposes of unit testing are:

1. **Validation of Code Functionality**: Unit tests ensure that each unit of the software performs as expected according to its specifications and requirements. By testing each unit in isolation, developers can identify and fix defects early in the development process, reducing the likelihood of bugs in the final product.

2. **Regression Testing**: Unit tests serve as a safety net against regressions - unintended changes or introductions of bugs in the codebase. Whenever modifications are made to the code, developers can rerun unit tests to ensure that existing functionality remains intact.

3. **Documentation**: Unit tests can serve as living documentation for the codebase. They provide examples of how individual units of code should be used and what behavior is expected from them.

4. **Facilitates Refactoring**: Unit tests enable developers to refactor code confidently. When refactoring, developers can rely on unit tests to ensure that changes do not introduce new defects or alter the intended behavior of the code.

5. **Promotes Modular and Testable Code**: Writing unit tests often leads to better software design by encouraging developers to write modular, decoupled, and testable code. Units that are difficult to test usually indicate design flaws, prompting developers to refactor and improve the design.

6. **Reduces Debugging Time**: Unit tests can help locate the source of bugs more quickly. When a unit test fails, developers can narrow down the scope of the problem to the specific unit being tested, making debugging more efficient.

Overall, unit testing is an essential practice in modern software development, promoting code quality, maintainability, and reliability throughout the development lifecycle.

Unit testing and functional testing serve different purposes in the software development process, and they operate at different levels of abstraction.

1. **Scope**:
   * **Unit Testing**: Focuses on testing individual units or components of the software, such as functions, methods, or classes, in isolation from the rest of the system. Unit tests verify the correctness of small, atomic units of code.
   * **Functional Testing**: Evaluates the functionality of the software as a whole by testing entire features or workflows. Functional tests verify that the software meets the specified requirements and behaves correctly from an end-user perspective.

2. **Isolation**:
   * **Unit Testing**: Units are tested in isolation, typically using mocks, stubs, or other forms of test doubles to simulate the behavior of dependencies. This isolation ensures that failures in unit tests are localized and easier to diagnose.
   * **Functional Testing**: Tests interactions between different components and modules, including external dependencies such as databases, APIs, or user interfaces. Functional tests evaluate the integration and behavior of the system as a whole.

3. **Granularity**:
   * **Unit Testing**: Tests are fine-grained and focus on verifying small, specific behaviors or functionalities within individual units of code.
   * **Functional Testing**: Tests are coarse-grained and assess larger features or functionalities, often spanning multiple units or modules of the system.

4. **Purpose**:
   * **Unit Testing**: Primarily aims to validate the correctness of the implementation of individual units of code, ensuring that each unit behaves as expected according to its specifications.
   * **Functional Testing**: Verifies that the software functions correctly from an end-user perspective, ensuring that it meets the intended requirements and provides the expected behavior and user experience.

5. **Timing**:
   * **Unit Testing**: Typically executed by developers during the development phase, often as part of a continuous integration (CI) process, to catch defects early and ensure code quality.
   * **Functional Testing**: Typically conducted by quality assurance (QA) engineers or testers during the testing phase, after the development of individual units or features, to assess the overall functionality and behavior of the software.

In summary, while unit testing focuses on testing small units of code in isolation to verify their correctness, functional testing evaluates the behavior and functionality of the software as a whole from an end-user perspective. Both types of testing are essential components of a comprehensive testing strategy and complement each other in ensuring the quality and reliability of software applications.

### How to test the code? What framework do you use?

Testing C++ code typically involves writing test cases that verify the correctness and robustness of your code. Here's a general approach to testing C++ code:

1. **Unit Testing**: Write individual test cases for each function or unit of code to ensure that they work as expected.

2. **Testing Frameworks**: Use testing frameworks like Google Test, Catch2, Boost.Test, or CppUnit to automate the testing process and manage test suites.

3. **Test Plan**: Develop a test plan outlining what aspects of the code you want to test and how you will test them.

4. **Test Coverage**: Aim for high test coverage to ensure that most, if not all, of your code is exercised by your tests.

5. **Boundary Cases**: Include test cases that cover boundary conditions, edge cases, and error conditions to ensure robustness.

6. **Regression Testing**: Re-run your tests whenever you make changes to the code to ensure that new changes do not introduce bugs or regressions.

7. **Integration Testing**: Test the interaction between different components/modules of your code to ensure they work together correctly.

8. **Performance Testing**: Evaluate the performance of your code under various conditions to ensure it meets your requirements.

Here's a simple example using Google Test, one of the popular testing frameworks for C++:

```cpp
// Code to be tested
int add(int a, int b) {
    return a + b;
}

// Test cases
#include <gtest/gtest.h>

TEST(AdditionTest, PositiveNumbers) {
    EXPECT_EQ(add(3, 4), 7);
    EXPECT_EQ(add(10, 20), 30);
}

TEST(AdditionTest, NegativeNumbers) {
    EXPECT_EQ(add(-3, -4), -7);
    EXPECT_EQ(add(-10, -20), -30);
}

TEST(AdditionTest, MixedNumbers) {
    EXPECT_EQ(add(-3, 4), 1);
    EXPECT_EQ(add(10, -20), -10);
}

int main(int argc, char **argv) {
    ::testing::InitGoogleTest(&argc, argv);
    return RUN_ALL_TESTS();
}
```

In this example:

* We have a simple `add` function that adds two integers.
* We write test cases using the Google Test framework to test the `add` function with different inputs.
* We run all the defined tests in the `main` function.

To compile and run the tests using Google Test, you would typically compile your code with the Google Test library and then execute the resulting binary:

```bash
g++ -std=c++11 your_code.cpp -lgtest -lgtest_main -pthread -o your_code_test
./your_code_test
```

This will execute the tests and display the results.

### What libraries do you know for writing tests?

There are several libraries available for writing tests in C++. Some of the most popular ones include:

1. **Google Test (gtest)**: Google's C++ testing framework, which provides a rich set of assertions and a powerful mocking framework. It's widely used in industry and has good documentation.

2. **Catch2**: A modern, header-only test framework for C++ that is known for its simplicity and expressive syntax. It's easy to set up and use, and it doesn't require any external dependencies.

3. **Boost.Test**: Part of the Boost libraries collection, Boost.Test provides a comprehensive set of tools for writing test cases and organizing test suites. It integrates well with other Boost libraries.

4. **doctest**: Another header-only testing framework for C++. It's known for its simplicity, speed, and ease of integration. It supports both traditional unit tests and behavior-driven development (BDD) style tests.

5. **CppUnit**: A framework for unit testing in C++, inspired by JUnit. It provides a rich set of assertion macros and supports fixture-based testing.

6. **UT**: A lightweight C++ unit testing framework that focuses on simplicity and minimalism. It's designed to be easy to integrate into projects and easy to use.

7. **TUT**: Another lightweight C++ unit testing framework that is particularly well-suited for embedded systems and other resource-constrained environments.

These are just a few examples, and there are many other testing frameworks and libraries available for C++ depending on your specific needs and preferences.

### What is a mock?

In programming, a "mock" refers to a simulated object or component used for testing purposes. When developing software, especially in environments that rely on various interconnected components, it's crucial to test the behavior of individual parts of the system. However, testing against real dependencies, such as databases, web services, or external APIs, can be cumbersome, slow, and sometimes impractical due to dependencies being unavailable or unpredictable.

Mocks serve as stand-ins for these dependencies, providing a controlled environment for testing. They mimic the behavior of real objects or components by responding to method calls or requests in predefined ways. Mocks are particularly useful in unit testing, where the goal is to isolate and test small units of code independently.

Mocking frameworks provide developers with tools to easily create and configure mock objects. These frameworks often offer features for defining expectations (specifying the behavior the mock should exhibit), verifying method calls, and managing complex interactions between different components of the system.

By using mocks, developers can achieve faster and more reliable testing, as they can focus solely on the code being tested without worrying about the behavior of external dependencies. Additionally, mocks facilitate testing in isolation, enabling developers to identify and fix bugs more efficiently.

Sure! Let's say you have a `Calculator` class with a dependency on a `Logger` class for logging messages. You want to test the `Calculator` class without relying on the actual `Logger` implementation. Instead, you can create a mock `Logger` class to simulate the behavior of the real `Logger` class.

Here's an example:

```cpp
#include <iostream>
#include <string>

// Logger interface
class Logger {
public:
    virtual void log(const std::string& message) = 0;
    virtual ~Logger() {} // virtual destructor for polymorphic behavior
};

// Mock Logger class
class MockLogger : public Logger {
public:
    void log(const std::string& message) override {
        std::cout << "Mock Logger: " << message << std::endl;
    }
};

// Calculator class with dependency on Logger
class Calculator {
private:
    Logger* logger;

public:
    Calculator(Logger* logger) : logger(logger) {}

    int add(int a, int b) {
        logger->log("Adding " + std::to_string(a) + " and " + std::to_string(b));
        return a + b;
    }
};

// Test function
void testCalculator() {
    MockLogger mockLogger; // Create mock logger
    Calculator calculator(&mockLogger); // Pass mock logger to Calculator

    int result = calculator.add(3, 5);
    std::cout << "Result: " << result << std::endl;
}

int main() {
    testCalculator();

    return 0;
}
```

In this example:

* We have a `Logger` interface defining a `log` method.
* We implement a `MockLogger` class that inherits from `Logger`, overriding the `log` method to simulate logging behavior.
* The `Calculator` class takes a `Logger` pointer in its constructor and uses it to log messages.
* In the `testCalculator` function, we create an instance of `MockLogger` and pass it to the `Calculator` constructor.
* When `testCalculator` calls `calculator.add(3, 5)`, the `Calculator` logs the message through the mock `Logger`.

This way, we can test the `Calculator` class independently of the actual logging implementation by using the mock `Logger`.

### How many tests should be written for one function?

The number of tests to be written for a function can vary depending on factors such as the complexity of the function, the expected behavior, and the level of confidence required in its correctness. However, a common guideline in software development is to aim for sufficient test coverage to thoroughly exercise the function under different scenarios and edge cases.

Here are some general principles to consider:

1. **Happy path**: Write tests that cover the typical use cases or the "happy path" of the function. These tests should validate that the function behaves as expected when provided with valid input.

2. **Edge cases**: Identify edge cases or boundary conditions relevant to the function's behavior and write tests to cover them. Examples include empty inputs, minimum and maximum values, null or undefined inputs, and so on.

3. **Error handling**: Test how the function handles invalid input or error conditions. Ensure that appropriate exceptions are thrown or error codes are returned when necessary.

4. **Corner cases**: Consider any unusual or unexpected scenarios that might occur and write tests to handle them. This might include situations where inputs are unexpected types, or where external dependencies behave unexpectedly.

5. **Performance**: In some cases, especially for performance-critical functions, it may be necessary to write tests to ensure that the function meets performance requirements under various load conditions.

6. **Refactoring**: If the function undergoes refactoring or changes, ensure that existing tests still provide adequate coverage and verify that the function's behavior remains unchanged.

There is no fixed rule for the exact number of tests required for a function, as it depends on factors such as the function's complexity and criticality. The goal should be to achieve a balance between ensuring thorough coverage and avoiding excessive redundancy. Test-driven development (TDD) practices often advocate for writing the minimum number of tests necessary to fully validate the function's behavior.

Sure, here's an example of a simple C++ function along with corresponding test cases using the Google Test framework:

```cpp
// Function to calculate the factorial of a non-negative integer
int factorial(int n) {
    if (n < 0)
        throw std::invalid_argument("Factorial is not defined for negative numbers");
    int result = 1;
    for (int i = 2; i <= n; ++i) {
        result *= i;
    }
    return result;
}
```

Now, let's write test cases for this function using Google Test:

```cpp
#include <gtest/gtest.h>

// Include the function to be tested
#include "factorial.h" // Assuming the function is defined in factorial.h

// Test case for positive integer input
TEST(FactorialTest, PositiveIntegerInput) {
    EXPECT_EQ(factorial(0), 1); // 0! = 1
    EXPECT_EQ(factorial(1), 1); // 1! = 1
    EXPECT_EQ(factorial(5), 120); // 5! = 120
    EXPECT_EQ(factorial(10), 3628800); // 10! = 3628800
}

// Test case for edge case (negative input)
TEST(FactorialTest, NegativeInput) {
    EXPECT_THROW(factorial(-1), std::invalid_argument);
}

// Test case for edge case (large input)
TEST(FactorialTest, LargeInput) {
    // 20! is a large number, but should still be within the range of int
    EXPECT_EQ(factorial(20), 2432902008176640000);
}

int main(int argc, char** argv) {
    testing::InitGoogleTest(&argc, argv);
    return RUN_ALL_TESTS();
}
```

In this example, we have three test cases:

1. `PositiveIntegerInput`: Tests the function with positive integer inputs to verify that it correctly computes the factorial.
2. `NegativeInput`: Tests whether the function correctly throws an exception when a negative input is provided.
3. `LargeInput`: Tests the function with a large input to verify that it can handle large factorials without overflow.

Each test case uses `EXPECT_EQ` to compare the expected result with the actual result of calling the `factorial` function. The `EXPECT_THROW` macro is used to verify that an exception is thrown when the function is called with a negative input. Finally, in the `main` function, we initialize Google Test and run all the test cases.

### 38. Discuss unit testing practices and frameworks in C++

Unit testing is a crucial aspect of software development aimed at ensuring the correctness and robustness of individual units of code. In C++, there are several popular unit testing frameworks and practices. Here are some commonly used ones:

1. **Google Test (gtest)**: Google Test is a widely used C++ testing framework developed by Google. It provides a comprehensive set of testing tools for writing and running C++ test cases, along with rich assertions for validating test results.

   * **Example**:

     ```cpp
     #include <gtest/gtest.h>

     TEST(TestCaseName, TestName) {
         // Test code here
         ASSERT_EQ(2 + 2, 4);
     }
     ```

2. **Catch2**: Catch2 is a modern, header-only C++ testing framework that is easy to set up and use. It offers a clean syntax for writing test cases and supports BDD-style testing.

   * **Example**:

     ```cpp
     #define CATCH_CONFIG_MAIN
     #include <catch2/catch.hpp>

     TEST_CASE("Adding numbers", "[math]") {
         REQUIRE(2 + 2 == 4);
     }
     ```

3. **Boost.Test**: Part of the Boost C++ libraries, Boost.Test is a powerful testing framework that provides various tools for writing and organizing test cases. It supports both automatic and manual test registration.

   * **Example**:

     ```cpp
     #define BOOST_TEST_MODULE MyTest
     #include <boost/test/included/unit_test.hpp>

     BOOST_AUTO_TEST_CASE(test_sum) {
         BOOST_CHECK(2 + 2 == 4);
     }
     ```

4. **CppUnit**: CppUnit is a C++ port of the famous JUnit framework for Java. It provides a framework for writing and executing unit tests in C++. Although it's slightly less popular compared to the other frameworks mentioned above, it's still used in some projects.

   * **Example**:

     ```cpp
     #include <cppunit/extensions/HelperMacros.h>
     class MyTest : public CppUnit::TestFixture {
         CPPUNIT_TEST_SUITE(MyTest);
         CPPUNIT_TEST(testSum);
         CPPUNIT_TEST_SUITE_END();

         public:
             void testSum() {
                 CPPUNIT_ASSERT(2 + 2 == 4);
             }
     };
     CPPUNIT_TEST_SUITE_REGISTRATION(MyTest);
     ```

5. **TUT**: TUT is a lightweight C++ unit testing framework designed for simplicity and ease of use. It provides a basic set of macros for writing test cases and doesn't have any external dependencies.

   * **Example**:

     ```cpp
     #include "tut.h"

     namespace {
         struct test_class {
             void test_method() {
                 ensure(2 + 2 == 4);
             }
         };

         typedef tut::test_group<test_class> factory;
         typedef factory::object object;
         factory tf("test");
         } // namespace
     ```

When choosing a unit testing framework for your C++ project, consider factors such as ease of use, integration with your development environment, community support, and compatibility with your project's requirements and constraints.
