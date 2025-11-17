---
DONE: true
DATE: 2025-08-22T16:57:00
---

## **Declaration**

- Tells the **compiler** that something (a variable, function, class…) exists.
    
- It does **not allocate storage** (for variables) and does **not provide implementation** (for functions).
    
- It's like making a **promise** that this thing will be defined somewhere else.

- Introduces the name, return type, and parameters to the compiler.

- Can appear **multiple times** in a program.

## **Definition**

- Actually **creates the object / function**.
    
- Allocates memory for variables.
    
- Provides the **implementation** for functions.

- Gives the compiler all information needed to generate machine code.

- Can appear **only once** in a program (per the One Definition Rule).

## Key Differences

| Aspect | Declaration | Definition |
|--------|-------------|------------|
| Memory Allocation | No | Yes |
| Implementation | No | Yes |
| Frequency | Multiple times allowed | Only once per program |
| Purpose | Tells compiler it exists | Creates the actual entity |

## Example: Functions

```cpp
#include <iostream>
using namespace std;

// Function declaration (also called prototype)
void add(int, int);

int main()
{
	add(10, 20);
	return 0;
}

// Function Definition
void add(int a, int b) 
{
	cout << (a + b) << endl;
}
```

## Example: Variables

```cpp
// Declaration (using extern keyword)
extern int myNumber;  // Declares but doesn't allocate memory

// Definition
int myNumber = 42;     // Defines and allocates memory
```

## The One Definition Rule (ODR)

The One Definition Rule is a fundamental C++ principle that states:

- **Non-inline functions** and **variables** can have only **one definition** in the entire program
- **Classes, structs, and templates** cannot have more than one definition per translation unit
- However, they can be **declared multiple times** 

### Why ODR Matters

Violating the ODR can lead to:
- Linker errors (multiple definition errors)
- Undefined behavior
- Difficult-to-diagnose bugs

### Best Practices

1. **Put declarations in header files** (.h or `.hpp`)
   - Function prototypes
   - Class declarations
   - extern variable declarations

1. **Put definitions in source files** (`.cpp`)
   - Function implementations
   - Variable definitions

3. **Use `extern` keyword** for global variables that need to be shared across files

4. **Inline functions** are exceptions - they can be defined in headers because each translation unit gets its own copy

## Common Use Cases

**Forward Declarations:**
- When you need to reference a function before it's defined
- When two functions need to call each other
- To reduce compile time by avoiding unnecessary includes

**Separating Interface from Implementation:**
- Declarations go in header files (interface)
- Definitions go in source files (implementation)
- This is fundamental to good C++ project organization

**External Linkage:**
```cpp
// file1.cpp
int globalVar = 100;  // Definition

// file2.cpp
extern int globalVar;  // Declaration - refers to the one in file1.cpp
```

## Important Notes

- Every definition is also a declaration, but not every declaration is a definition
- Don't confuse **definition** with **initialization** (initialization is giving an initial value)
- Function declarations are often called **prototypes** or **forward declarations**
- Declarations allow the compiler to check if you're using functions correctly before it sees the full definition