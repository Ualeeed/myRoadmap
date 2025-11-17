---
DONE: true
DATE: 2025-08-23T08:27:00
---

# **What is `try-catch`?**

In modern C++, in most scenarios, the preferred way to report and handle both logic errors and runtime errors is to use exceptions. `try-catch` is used to **handle errors or exceptional situations** in a program gracefully.

Instead of the program crashing, you can **catch exceptions** and handle them in a controlled manner, allowing your program to continue running or terminate gracefully.

## **Basic Syntax**

```cpp
#include <iostream>
#include <vector>
#include <stdexcept>

using namespace std;

int main() 
{
    vector<int> num{1, 2, 3, 4, 5};

    try {
        // Code that might throw an exception
        cout << num.at(5) << endl;  // This will throw std::out_of_range
    }
    catch (const std::out_of_range& e) {
        cout << "Caught out_of_range exception: " << e.what() << endl;
    }
    catch (const std::exception& e) {
        cout << "Caught general exception: " << e.what() << endl;
    }
    catch (...) {
        cout << "Caught unknown exception" << endl;
    }

    return 0;
}
```

## **Key Components**

### **1. `try` Block**
- Contains code that might throw an exception
- If an exception occurs, control immediately transfers to the appropriate catch block

### **2. `catch` Block**
- Handles specific types of exceptions
- Throw exceptions by value, catch them by reference
- Multiple catch blocks can handle different exception types

### **3. `throw` Statement**
```cpp
void validateAge(int age) {
    if (age < 0) {
        throw std::invalid_argument("Age cannot be negative");
    }
    if (age > 150) {
        throw std::out_of_range("Age seems unrealistic");
    }
}
```

## **Standard Exception Hierarchy**

C++ provides a rich hierarchy of standard exceptions that inherit from `std::exception`:

```cpp
#include <stdexcept>

try {
    // Various operations that might throw
    std::vector<int> v;
    v.at(100);  // throws std::out_of_range
    
    std::string s = "hello";
    int num = std::stoi(s);  // throws std::invalid_argument
}
catch (const std::out_of_range& e) {
    cout << "Out of range: " << e.what() << endl;
}
catch (const std::invalid_argument& e) {
    cout << "Invalid argument: " << e.what() << endl;
}
catch (const std::exception& e) {
    cout << "Standard exception: " << e.what() << endl;
}
```

## **Modern C++ Best Practices**

### **1. Exception Safety Guarantees**
The following four levels of exception guarantee are generally recognized:
- **Nothrow guarantee**: Function never throws exceptions
- **Strong guarantee**: If exception thrown, program state unchanged
- **Basic guarantee**: If exception thrown, program remains in valid state
- **No guarantee**: If exception thrown, program state is undefined

### **2. `noexcept` Specifier** 
The noexcept specifier has an optional Boolean parameter. noexcept(true) is equivalent to noexcept, meaning the function is non-throwing:

```cpp
// Function guaranteed not to throw
int safeFunction() noexcept {
    return 42;
}

// Function may throw (default behavior)
int riskyFunction() noexcept(false) {
    throw std::runtime_error("Something went wrong");
}
```

### **3. Custom Exception Classes**
We recommend that you derive your own exception class from std::exception:

```cpp
class DatabaseError : public std::runtime_error {
public:
    DatabaseError(const std::string& msg) : std::runtime_error(msg) {}
};

class NetworkError : public std::runtime_error {
public:
    NetworkError(const std::string& msg) : std::runtime_error(msg) {}
};

// Usage
try {
    connectToDatabase();
}
catch (const DatabaseError& e) {
    cout << "Database issue: " << e.what() << endl;
}
catch (const NetworkError& e) {
    cout << "Network issue: " << e.what() << endl;
}
```

## **Advanced Exception Handling Patterns**

### **1. RAII (Resource Acquisition Is Initialization)**
```cpp
#include <memory>
#include <fstream>

void processFile(const std::string& filename) {
    auto file = std::make_unique<std::ifstream>(filename);
    if (!file->is_open()) {
        throw std::runtime_error("Cannot open file: " + filename);
    }
    
    // Even if exception occurs, file will be automatically closed
    // when unique_ptr goes out of scope
    processFileContent(*file);
}
```

### **2. Exception Chaining and Rethrowing**
```cpp
void lowLevelFunction() {
    try {
        // Some operation
        riskyOperation();
    }
    catch (const std::exception& e) {
        // Log the error and rethrow
        logError("Error in lowLevelFunction: " + std::string(e.what()));
        throw;  // Rethrows the original exception
    }
}
```

## **Common Pitfalls to Avoid**

There are several common mistakes to avoid when implementing exception handling:

1. **Don't use exceptions for regular control flow**
2. **Don't catch and ignore exceptions without proper handling**
3. **Don't throw exceptions from destructors**
4. **Don't use bare `catch(...)` without good reason**

```cpp
// BAD: Using exceptions for control flow
try {
    for (int i = 0; ; ++i) {
        cout << vec.at(i) << " ";  // Will throw when out of bounds
    }
}
catch (...) {
    // This is abuse of exception handling
}

// GOOD: Proper bounds checking
for (size_t i = 0; i < vec.size(); ++i) {
    cout << vec[i] << " ";
}
```

## **When to Use Exceptions**

As a general rule of thumb, throw an exception when your program can identify an external problem that prevents execution:

- **Use exceptions for**: Unexpected conditions, resource unavailability, invalid input that can't be handled locally
- **Don't use exceptions for**: Expected conditions, performance-critical code paths, simple validation

## **Performance Considerations**

- Exception handling has zero overhead when no exceptions are thrown
- When exceptions are thrown, there is significant overhead
- Use `noexcept` to help compiler optimize code
- Consider alternatives like `std::optional` or error codes for frequently occurring error conditions

This comprehensive approach to exception handling helps create robust, maintainable C++ programs that can gracefully handle unexpected situations while maintaining good performance characteristics.