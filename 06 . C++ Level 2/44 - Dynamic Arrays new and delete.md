---
DONE: true
DATE: 2025-08-23T07:57:00
---

Dynamic arrays are arrays whose size is determined at runtime rather than compile time. They provide flexibility when you don't know the exact size needed beforehand, such as when the size depends on user input or other runtime calculations.

## What is a Dynamic Array?

A **dynamic array** is an array with the following characteristics:
- **Size determined at runtime** - you can specify the size during program execution
- **Allocated on the heap** - uses dynamic memory allocation
- **Flexible sizing** - unlike static arrays, the size doesn't need to be a compile-time constant
- **Manual memory management** - requires explicit allocation and deallocation

## Memory Allocation: Stack vs Heap

### Stack Allocation (Static Arrays)
```c++
int staticArray[10];  // Size must be known at compile time
```
- Fast allocation/deallocation
- Automatic cleanup when out of scope
- Limited size (stack memory is limited)

### Heap Allocation (Dynamic Arrays)
```c++
int* dynamicArray = new int[size];  // Size can be determined at runtime
```
- Slower allocation/deallocation
- Manual memory management required
- Larger available memory space

## Syntax and Basic Operations

### Allocation Syntax
```cpp
Type* arrayName = new Type[size];   // Allocate memory
delete[] arrayName;                 // Free memory
```

**Components:**
- `Type*` → Pointer to the first element of the array
- `new Type[size]` → Allocates memory for `size` elements of `Type`
- `delete[]` → Deallocates memory for the entire array

### Basic Example
```cpp
#include <iostream>
using namespace std;

int main() {
    int size;
    cout << "Enter array size: ";
    cin >> size;
    
    // Allocate dynamic array
    int* arr = new int[size];
    
    // Use the array
    for (int i = 0; i < size; i++) {
        arr[i] = i + 1;
        cout << arr[i] << " ";
    }
    cout << endl;
    
    // Free memory
    delete[] arr;
    arr = nullptr;  // Good practice to avoid dangling pointer
    
    return 0;
}
```

## Comprehensive Example: Student Grades System

```cpp
#include <iostream>
using namespace std;

int main() {
    int num;
    cout << "Enter total number of students: ";
    cin >> num;

    // Check for valid input
    if (num <= 0) {
        cout << "Invalid number of students!" << endl;
        return 1;
    }

    // Memory allocation for num number of floats
    float* ptr = new float[num];

    // Input grades
    cout << "Enter grades of students:" << endl;
    for (int i = 0; i < num; i++) {
        cout << "Student " << i + 1 << ": ";
        cin >> *(ptr + i);  // Equivalent to ptr[i]
    }

    // Display grades
    cout << "\nDisplaying grades of students:" << endl;
    for (int i = 0; i < num; i++) {
        cout << "Student " << i + 1 << ": " << *(ptr + i) << endl;
    }

    // Calculate average
    float sum = 0;
    for (int i = 0; i < num; i++) {
        sum += ptr[i];
    }
    cout << "Average grade: " << sum / num << endl;

    // Free memory and set pointer to null
    delete[] ptr;
    ptr = nullptr;

    return 0;
}
```

## Memory Management Best Practices

### 1. Always Free Allocated Memory
Not deallocating memory properly can cause memory leaks which in turn causes the program to consume a large amount of memory.

```cpp
int* arr = new int[100];
// ... use array ...
delete[] arr;  // Essential to prevent memory leaks
```

### 2. Set Pointers to `nullptr` After Deletion
It is a good practice to set pointer to `nullptr` after deallocating the memory to avoid undefined behavior if the pointer is dereferenced.

```c++
delete[] arr;
arr = nullptr;  // Prevents accidental use of dangling pointer
```

### 3. Check for Allocation Failures
It is considered good practice for programs to always be able to handle failures to allocate memory, either by checking the pointer value (if nothrow) or by catching the proper exception.

```cpp
int* arr = new(nothrow) int[size];
if (arr == nullptr) {
    cout << "Memory allocation failed!" << endl;
    return 1;
}
```

## Common Mistakes and How to Avoid Them

### 1. Memory Leaks
**Problem:** Forgetting to call `delete[]`
```cpp
void badFunction() {
    int* arr = new int[1000];
    // Function ends without delete[] - MEMORY LEAK!
}
```

**Solution:** Always match `new[]` with `delete[]`
```cpp
void goodFunction() {
    int* arr = new int[1000];
    // ... use array ...
    delete[] arr;
    arr = nullptr;
}
```

### 2. Dangling Pointers
**Problem:** Using a pointer after memory has been freed
```cpp
int* arr = new int[10];
delete[] arr;
arr[0] = 5;  // UNDEFINED BEHAVIOR - accessing freed memory
```

**Solution:** Set pointer to nullptr after deletion
```cpp
int* arr = new int[10];
delete[] arr;
arr = nullptr;
// Now arr[0] would cause immediate crash instead of undefined behavior
```

### 3. Using `delete` Instead of `delete[]`
**Problem:** For arrays, use new[] and delete[]. For single variables, use new and delete.
```c++
int* arr = new int[10];
delete arr;  // WRONG! Should be delete[]
```

**Solution:** Always use `delete[]` for arrays
```c++
int* arr = new int[10];
delete[] arr;  // CORRECT
```

### 4. Double Deletion
**Problem:** Deleting the same memory twice
```c++
int* arr = new int[10];
delete[] arr;
delete[] arr;  // UNDEFINED BEHAVIOR
```

**Solution:** Set to nullptr after first deletion
```cpp
int* arr = new int[10];
delete[] arr;
arr = nullptr;
delete[] arr;  // Safe - deleting nullptr is allowed
```

## When to Use Dynamic Arrays

### Good Use Cases:
- Size depends on user input or runtime calculations
- Working with large datasets that might exceed stack limits
- Need to pass arrays between functions with varying sizes
- Building data structures like dynamic lists

### Consider Alternatives:
- **std::vector** - Safer, automatic memory management
- **std::array** - For compile-time known sizes
- **Static arrays** - For small, fixed-size arrays

## Memory Layout Visualization

```
Stack Memory:        Heap Memory:
+-----------+       +---+---+---+---+---+
|    ptr    |------>| 1 | 2 | 3 | 4 | 5 |  (Dynamic array)
+-----------+       +---+---+---+---+---+
```

The pointer `ptr` is stored on the stack, but it points to memory allocated on the heap where the actual array data resides.

## Key Takeaways

1. **Dynamic arrays provide runtime flexibility** but require careful memory management
2. **Always pair `new[]` with `delete[]`** to prevent memory leaks
3. **Set pointers to nullptr after deletion** to avoid dangling pointer issues
4. **Check for allocation failures** in production code
5. **Consider using std::vector** for safer dynamic array operations
6. **Dynamically allocated memory has dynamic duration and will stay allocated until you deallocate it or the program terminates**

*Dynamic arrays are a powerful feature in C++, but with great power comes great responsibility. Proper memory management is crucial for writing robust, efficient programs.
