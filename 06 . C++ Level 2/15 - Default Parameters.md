---
DONE: true
DATE: 2025-08-22T17:00:00
---

## What are Default Parameters?

A <span style="color:rgb(181, 75, 251)">default parameter</span> is a value that is automatically assigned to a function parameter if the caller of the function does not provide a value for it.

When a function with default arguments is called without passing arguments, the default parameters are used, but if arguments are passed while calling the function, the default arguments are ignored.

## Rules for Default Parameters

1. **Default values are defined in the function declaration** (usually in the header) or in the first declaration if there is both a declaration and definition.
    
2. **Once a parameter has a default value, all parameters to its right must also have default values.** 

Example:

```cpp
void func(int a = 1, int b); // ❌ Not allowed
void func(int a, int b = 2); // ✅ Allowed
```

3. **Default arguments cannot be redefined** - Once specified in a declaration, they cannot be changed in the definition.

4. **Default arguments are evaluated at call time** - Each time the function is called without an argument, the default value is evaluated.

5. **Put defaults in forward declarations, not definitions** - The best practice is to declare the default argument in the forward declaration and not in the function definition, as the forward declaration is more likely to be seen by other files.

## Basic Example

```cpp
#include <iostream>
using namespace std;

int MySum(int a, int b, int c = 0, int d = 0) 
{
	return (a + b + c + d);
}

int main() 
{
	cout << MySum(10, 20) << endl;        // Uses default c=0, d=0
	cout << MySum(10, 20, 30) << endl;     // Uses default d=0
	cout << MySum(10, 20, 30, 40) << endl; // No defaults used

	return 0;
}
```

**Output:**
```
30
60
100
```

## Advanced Examples

### Example 1: String Default Parameter

```cpp
void greet(string name = "Guest") 
{
	cout << "Hello, " << name << "!" << endl;
}

int main() 
{
	greet("Alice");  // Output: Hello, Alice!
	greet();         // Output: Hello, Guest!
	return 0;
}
```

### Example 2: Multiple Default Parameters

```cpp
void displayInfo(string name, int age = 18, string city = "Unknown") 
{
	cout << "Name: " << name << endl;
	cout << "Age: " << age << endl;
	cout << "City: " << city << endl;
}

int main() 
{
	displayInfo("John");                    // Uses both defaults
	displayInfo("Sarah", 25);               // Uses city default
	displayInfo("Mike", 30, "New York");    // No defaults
	return 0;
}
```

### Example 3: Using Previous Parameters in Defaults

```cpp
 int calculate(int x, int y = x * 2)  // y defaults to twice x
 {
	return x + y;
 }
```

**Note:** Earlier parameters can be used in default values of later parameters.

## Common Use Cases

**1. Simplifying Function Calls**
- Provide sensible defaults for commonly-used values
- Reduce the number of overloaded functions needed

**2. Backward Compatibility**
- Add new parameters to existing functions without breaking existing code

**3. Configuration Functions**
- Settings that usually stay at standard values but can be customized

**4. Mathematical Functions**
- Precision levels, rounding modes, or calculation methods with standard defaults

## Best Practices

✅ **DO:**
- Use default parameters for values that rarely change
- Place default parameters at the end of the parameter list
- Use meaningful default values that make sense in most contexts
- Document what the default values mean
- Keep default values simple (constants or simple expressions)

❌ **DON'T:**
- Overuse default parameters - too many can make code unclear
- Use default parameters when the value should always be explicitly specified
- Create complex expressions as default values
- Mix default parameters with function overloading excessively

## Common Pitfalls

**1. Cannot Skip Parameters**
```cpp
void func(int a, int b = 2, int c = 3);

func(1, , 5);  // ❌ Cannot skip b to provide c
func(1, 2, 5); // ✅ Must provide b if you want to provide c
```

**2. Virtual Functions Caution**
Default arguments are bound at compile-time, not run-time. This can cause unexpected behavior with virtual functions.

**3. Header/Source File Mismatch**
```cpp
// header.h
void func(int a = 10);  // ✅ Declaration with default

// source.cpp
void func(int a = 10)   // ❌ Don't repeat default in definition
{
	// implementation
}
```

## Advantages

- Reduces code duplication
- Makes functions more flexible
- Improves code readability
- Simplifies API usage
- Provides backward compatibility

## Disadvantages

- Can make interfaces less natural because arguments are no longer grouped in logical order
- May hide important decisions that should be explicit
- Can lead to confusion about what values are actually being used
- Harder to refactor when default values need to change

## Default Parameters vs Function Overloading

Both can achieve similar results, but:

**Use Default Parameters when:**
- The logic is identical for all cases
- You want to provide optional configuration

**Use Function Overloading when:**
- Different parameter counts require different logic
- You want stronger type checking
- The operations are conceptually different