---
DONE: true
DATE: 2025-08-22T23:31:00
---

A **vector** 
is a fundamental container in the C++ <mark style="background: #D33AFFA6;">Standard Template Library</mark> (STL) that provides **dynamic array** capabilities. Unlike fixed-size C-style arrays, <span style="color:rgb(0, 176, 80)">vectors</span> can automatically **grow or shrink** in size as elements are added or removed, handling memory management internally. This makes them highly versatile for various programming tasks.

To use `std::vector`, you need to include the `<vector>` header file.

### Declaration and Initialization

Vectors can be declared and initialized in several ways:

*   **Empty vector:** 
 ```c++
   std::vector<int> myVector;
 ```
*   **With a specified size and default values:** 
```c++
   std::vector<int> myVector(10); // creates a vector of 10 integers, initialized to 0
```
*   **With a specified size and initial value:** 
```c++
   std::vector<int> myVector(5, 100); // creates a vector of 5 integers, all initialized to 100
```
*   **Using an initializer list:** 
```c++
   std::vector<int> myVector = {1, 2, 3, 4, 5};
```
*   **From another vector (copy constructor):**
```c++
   std::vector<int> anotherVector = {1, 2, 3};
   std::vector<int> myVector(anotherVector);
```
*   **From a range (e.g., another vector or array):** 
```c++
   int arr[] = {10, 20, 30};
   std::vector<int> myVector(arr, arr + 3);
```

### Common Operations

Here are some frequently used operations with `std::vector`:

*   **Adding elements:**
    *   `push_back(value)`: Adds an element to the end of the vector.
    *   `insert(position, value)`: Inserts an element at a specific position.

*   **Accessing elements:**
    *   `myVector[index]`: Provides direct access to an element at a given index (no bounds checking).
    *   `myVector.at(index)`: Accesses an element at a given index with bounds checking.
    *   `front()`: Returns a reference to the first element.
    *   `back()`: Returns a reference to the last element.

*   **Changing elements:**
    *   Elements can be changed using either `myVector[index] = newValue;` or `myVector.at(index) = newValue;`.

*   **Removing elements:**
    *   `pop_back()`: Removes the last element from the vector.
    *   `erase(iterator)`: Removes the element pointed to by the iterator.
    *   `clear()`: Removes all elements from the vector, making it empty.

*   **Size and Capacity:**
    *   `size()`: Returns the number of elements currently in the vector.
    *   `capacity()`: Returns the total number of elements the vector can hold before it needs to reallocate memory.
    *   `empty()`: Returns `true` if the vector contains no elements, `false` otherwise.
    *   `resize(n)`: Changes the number of elements stored in the vector to `n`.
    *   `reserve(n)`: Requests that the vector capacity be at least `n`.
    *   `shrink_to_fit()`: Reduces the capacity of the vector to fit its current size.

*   **Iterators:**
    *   `begin()`: Returns an iterator pointing to the first element.
    *   `end()`: Returns an iterator pointing to the theoretical element *after* the last element.

### Example

```cpp
#include <iostream>
#include <vector>
#include <numeric> // For std::iota

int main() {
    // Declare and initialize a vector of integers
    std::vector<int> numbers = {10, 20, 30, 40, 50};

    std::cout << "Initial vector elements: ";
    for (int num : numbers) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    // Add an element to the end
    numbers.push_back(60);
    std::cout << "After push_back(60): ";
    for (int num : numbers) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    // Access elements
    std::cout << "Element at index 0: " << numbers[0] << std::endl;
    std::cout << "Element at index 2 using at(): " << numbers.at(2) << std::endl;

    // Change an element
    numbers[1] = 25;
    std::cout << "After changing element at index 1 to 25: ";
    for (int num : numbers) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    // Remove the last element
    numbers.pop_back();
    std::cout << "After pop_back(): ";
    for (int num : numbers) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    // Get size and capacity
    std::cout << "Current size: " << numbers.size() << std::endl;
    std::cout << "Current capacity: " << numbers.capacity() << std::endl;

    // Insert an element at a specific position (before index 2)
    numbers.insert(numbers.begin() + 2, 35);
    std::cout << "After inserting 35 at index 2: ";
    for (int num : numbers) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    // Erase an element (at index 3)
    numbers.erase(numbers.begin() + 3);
    std::cout << "After erasing element at index 3: ";
    for (int num : numbers) {
        std::cout << num << " ";
    }
    std::cout << std::endl;

    // Clear all elements
    numbers.clear();
    std::cout << "After clear(), size: " << numbers.size() << std::endl;

    // Check if empty
    if (numbers.empty()) {
        std::cout << "Vector is empty." << std::endl;
    }

    return 0;
}
```

