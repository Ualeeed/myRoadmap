---
Date: 2025-08-23
DONE: true
---

# Common Mistakes with Pointers in C++

## 1. Using an Uninitialized Pointer

Uninitialized pointers contain garbage values that can point to any memory location, leading to undefined behavior.

```cpp
int *p;       // uninitialized (garbage address)
*p = 10;      // ❌ Undefined behavior (may crash)
```

**Solution:** Always initialize pointers:
```cpp
int *p = nullptr;  // safe initialization
```

## 2. Confusion Between Pointer Address and Value

```cpp
#include <iostream>
using namespace std;

int main() {
    int x, *p;
    
    // ❌ Wrong! p expects an address, but x is a value
    p = x;
    
    // ✅ Correct! p gets the address of x
    p = &x;
    
    // ❌ Wrong! *p expects a value, but &x is an address
    *p = &x;
    
    // ✅ Correct! *p gets the value of x
    *p = x;
    
    return 0;
}
```

## 3. Dangling Pointers

A dangling pointer occurs when a pointer continues to reference a memory location after the memory has been freed or deallocated.

```cpp
int* create_dangling_pointer() {
    int x = 5;
    return &x;  // ❌ Returning pointer to local variable
}

int* ptr = new int(42);
delete ptr;
*ptr = 10;  // ❌ Using pointer after deletion
```

**Solutions:**
- Set pointers to `nullptr` after deletion
- Use smart pointers for automatic memory management
- Avoid returning pointers to local variables

## 4. Double Free/Delete

This error occurs when we try and free a specific dynamically allocated memory more than once.

```cpp
int *p1 = new int(10);
int *p2 = p1;  // Both point to same memory

delete p1;
delete p2;     // ❌ Double deletion - undefined behavior
```

**Solution:** Set pointers to `nullptr` after deletion:
```c++
delete p1;
p1 = nullptr;
p2 = nullptr;  // Or track ownership carefully
```

## 5. Memory Leaks

```cpp
void memory_leak_example() {
    int *ptr = new int(42);
    // Function returns without delete
    // ❌ Memory leak - allocated memory never freed
}
```

## 6. Array Bounds Violation

```c++
int arr[5];
int *ptr = arr;
ptr[10] = 42;  // ❌ Writing beyond array bounds
```

## 7. Incorrect Pointer Declaration Style

In declarations like `int* ptr1, ptr2;`, only ptr1 is a pointer — ptr2 is just an int.

```cpp
int* ptr1, ptr2;  // ❌ Confusing: only ptr1 is a pointer
int* ptr1;        // ✅ Clear: declare one pointer per line
int* ptr2;
```

## Modern C++ Best Practices

### Use Smart Pointers

Prefer smart pointers (unique_ptr, shared_ptr) over raw pointers and use `std::make_unique` and `std::make_shared` for exception safety.

```cpp
#include <memory>

// Instead of raw pointers:
int* raw_ptr = new int(42);  // ❌ Manual memory management

// Use smart pointers:
auto smart_ptr = std::make_unique<int>(42);  // ✅ Automatic cleanup
```

### RAII Principle

Smart pointers follow the Resource Acquisition Is Initialization (RAII) principle, which ties resource management to object lifetime.

```cpp
void safe_function() {
    auto ptr = std::make_unique<int[]>(1000);
    // Automatic cleanup when ptr goes out of scope
}
```

### Key Takeaways

1. **Always initialize pointers** - Use `nullptr` for safe initialization
2. **Understand the difference** between pointer addresses (`&variable`) and values (`*pointer`)
3. **Avoid dangling pointers** - Don't use pointers after the memory is freed
4. **Prevent double deletion** - Set pointers to `nullptr` after deletion
5. **Use smart pointers** - Let C++ manage memory automatically
6. **Follow RAII** - Tie resource management to object lifetime
7. **Check array bounds** - Ensure you don't access memory beyond allocated space

By following these best practices, you can use pointers effectively and safely in your programs. Remember to always initialize and verify your pointers, use appropriate bounds checking, and release dynamically allocated memory when you are done with it.
