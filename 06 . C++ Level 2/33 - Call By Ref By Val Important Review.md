---
DONE: true
DATE: 2025-08-23T06:36:00
---

## Parameter Passing in C++

### **1. Call by Value**

- **What happens:** A copy of the actual value is passed to the function.
    
- **Effect:** Changes made inside the function **do not affect** the original variable.
    
- **Memory use:** Requires extra memory for the copy.
    
- **Safe:** The original variable is protected from modifications.

- **When to use:** 
  - For small, primitive types ` (int, float, double, char)` 
  - When you don't want the function to modify the original value
  - When the data is small enough that copying is not expensive

#### Example - Call by Value:

```cpp
#include <iostream>

using namespace std;

void Function1(int x)
{
	x++;  // This only modifies the copy, not the original
}

int main()
{
	int a = 10;
	Function1(a);
	cout << "\n a after calling function1 = " << a << endl;  // Output: 10
	return 0;
}
```

**Output:** `a after calling function1 = 10`

---

### **2. Call by Reference**

- **What happens:** The function gets the **address/reference** of the variable.
    
- **Effect:** Changes made inside the function **directly affect** the original variable.
    
- **Memory use:** No extra copy is created, so it's faster for large objects.
    
- **Risky:** The original variable can be accidentally modified.

- **When to use:**
  - When you need the function to modify the original variable
  - For large objects (strings, vectors, custom classes) to avoid expensive copying
  - When returning multiple values from a function

#### Example - Call by Reference:

```cpp
#include <iostream>

using namespace std;

void Function1(int &x)
{
	x++;  // This modifies the original variable
}

int main()
{
	int a = 10;
	Function1(a);
	cout << "\n a after calling function1 = " << a << endl;  // Output: 11
	return 0;
}
```

**Output:** `a after calling function1 = 11`

---

### **3. Call by Const Reference (Best of Both Worlds)**

- **What happens:** The function gets a reference to the variable, but **cannot modify it**.
    
- **Effect:** Changes are **not allowed** - compiler will give an error if you try to modify.
    
- **Memory use:** No copy is created (efficient for large objects).
    
- **Safe:** The original variable is protected from modifications.

- **When to use:**
  - For large objects (vectors, strings, classes) when you only need to read the data
  - Best practice for passing read-only parameters efficiently
  - Combines the efficiency of pass-by-reference with the safety of pass-by-value

#### Example - Call by Const Reference:

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;

// Efficient: no copying, but cannot modify
void PrintVector(const vector<int>& v)
{
	for(int num : v) {
		cout << num << " ";
	}
	cout << endl;
	// v.push_back(10);  // ERROR: Cannot modify const reference!
}

void PrintString(const string& str)
{
	cout << str << endl;
	// str[0] = 'X';  // ERROR: Cannot modify const reference!
}

int main()
{
	vector<int> numbers = {1, 2, 3, 4, 5};
	string message = "Hello, World!";
	
	PrintVector(numbers);  // Efficient - no copying
	PrintString(message);  // Efficient - no copying
	
	return 0;
}
```

---

### **Comparison Table**

| Feature | Call by Value | Call by Reference | Call by Const Reference |
|---------|--------------|-------------------|------------------------|
| **Creates copy?** | Yes | No | No |
| **Can modify original?** | No | Yes | No |
| **Memory efficient?** | No (for large objects) | Yes | Yes |
| **Safe from modification?** | Yes | No | Yes |
| **Best for** | Small types (int, float) | When modification needed | Large read-only objects |
| **Syntax** | `void func(int x)` | `void func(int &x)` | `void func(const int &x)` |

---

### **Understanding References and Addresses**

```cpp
#include <iostream>

using namespace std;

int main()
{
	int a = 10;

	cout << "Value of a = " << a << endl;
	cout << "Address/Reference of a = " << &a << endl;

	return 0;
}
```

**Output:**
```
Value of a = 10
Address/Reference of a = 0x7ffd5c3e9a1c  // (address will vary)
```

---

### **Performance Considerations**

```ad-success
title: Best Practices for Parameter Passing
1. **Small primitive types (int, float, double, char, bool):** Pass by value
   ```cpp
   void calculate(int x, double y) { }  // ✓ Good
   ```

2. **Large objects (vectors, strings, custom classes) - read only:** Pass by const reference
   ```cpp
   void display(const vector<int>& v) { }  // ✓ Good (efficient & safe)
   void display(vector<int> v) { }         // ✗ Bad (expensive copy)
   ```

3. **When you need to modify the original:** Pass by reference
   ```cpp
   void increment(int& x) { x++; }  // ✓ Good (modifies original)
   ```

4. **When returning multiple values:** Pass by reference
   ```cpp
   void getMinMax(const vector<int>& v, int& min, int& max) {
       // Find min and max, modify the references
   }
   ```


### **Common Mistakes to Avoid**

```ad-danger
title: Warning
1. **Passing large objects by value unnecessarily:**
	
	
	
	

   ```
   
   ```cpp
   
   // ✗ BAD - Creates expensive copy
   void processVector(vector<int> v) { }
   
   // ✓ GOOD - No copy, efficient
   void processVector(const vector<int>& v) { }
   ```

2. **Using non-const reference when you don't need to modify:**
   ```cpp
   // ✗ BAD - Allows accidental modification
   void display(vector<int>& v) { }
   
   // ✓ GOOD - Prevents accidental modification
   void display(const vector<int>& v) { }
   ```

3. **Returning reference to local variable:**
   ```cpp
   // ✗ DANGEROUS - Returns reference to destroyed variable
   int& badFunction() {
       int x = 10;
       return x;  // x will be destroyed after function ends!
   }
   ```


---

### **Practical Example - Multiple Return Values**

```cpp
#include <iostream>
#include <vector>

using namespace std;

// Using references to return multiple values
void findMinMax(const vector<int>& numbers, int& minVal, int& maxVal)
{
	if(numbers.empty()) return;
	
	minVal = maxVal = numbers[0];
	
	for(int num : numbers) {
		if(num < minVal) minVal = num;
		if(num > maxVal) maxVal = num;
	}
}

int main()
{
	vector<int> data = {15, 3, 27, 8, 42, 11};
	int minimum, maximum;
	
	// Pass by const reference (read-only) and by reference (to modify)
	findMinMax(data, minimum, maximum);
	
	cout << "Minimum: " << minimum << endl;  // 3
	cout << "Maximum: " << maximum << endl;  // 42
	
	return 0;
}
```

---

### **Quick Decision Guide**

```
                    Need to modify original?
                    /                    \
                  YES                    NO
                   |                      |
            Pass by Reference       Is it a small type?
            void func(T& x)        /              \
                                 YES               NO
                                  |                 |
                           Pass by Value    Pass by Const Ref
                           void func(T x)   void func(const T& x)
```

**Small types:** int, float, double, char, bool, pointers  
**Large types:** string, vector, array, custom classes/structs

---

### **Memory Visualization**

```cpp
// Call by Value
void byValue(int x) {
    x = 20;  // Changes copy only
}
int a = 10;
byValue(a);
// Memory: [a: 10] [copy of a: 20] → a remains 10

// Call by Reference  
void byReference(int& x) {
    x = 20;  // Changes original
}
int a = 10;
byReference(a);
// Memory: [a: 20] → a is modified to 20

// Call by Const Reference
void byConstRef(const int& x) {
    // x = 20;  // ERROR! Cannot modify
    cout << x;  // Can only read
}
int a = 10;
byConstRef(a);
// Memory: [a: 10] → a remains 10, but no copy made
```
