---
DONE: true
DATE: 2025-08-23T00:37:00
---

#### Adding Elements: 

| Function            | Description                         | Example                        |
| ------------------- | ----------------------------------- | ------------------------------ |
| `push_back(x)`      | Adds element at the end             | `v.push_back(20);`             |
| `emplace_back(x)`   | Constructs element in-place at end (more efficient) | `v.emplace_back(20);` |
| `insert(pos, x)`    | Insert element at specific position | `v.insert(v.begin() + 1, 15);` |
| `insert(pos, n, x)` | Insert n copies of x at pos         | `v.insert(v.begin(), 3, 5);`   |
| `emplace(pos, x)`   | Constructs element in-place at position | `v.emplace(v.begin() + 1, 15);` |

```ad-tip
title: emplace vs push_back
`emplace_back()` constructs the element directly in the vector's memory, while `push_back()` creates a temporary object first and then copies/moves it. For simple types they're similar, but `emplace_back()` can be more efficient for complex objects.
```

#### Removing Elements:

|Function|Description|Example|
|---|---|---|
|`pop_back()`|Remove last element|`v.pop_back();`|
|`erase(pos)`|Remove element at position|`v.erase(v.begin() + 1);`|
|`erase(start, end)`|Remove a range of elements|`v.erase(v.begin(), v.begin() + 2);`|
|`clear()`|Remove all elements|`v.clear();`|

#### Accessing Elements: 

|Function|Description|Example|
|---|---|---|
|`v[i]`|Access element at index i|`v[0]`|
|`v.at(i)`|Access with bounds checking|`v.at(2)`|
|`front()`|First element|`v.front()`|
|`back()`|Last element|`v.back()`|
|`data()`|Pointer to underlying array|`int* ptr = v.data();`|

```ad-attention
title: Important
#### **What `v.data()` does**

- Every `vector` stores its elements **in a contiguous block of memory**, just like a normal array.
    
- `v.data()` **returns a pointer to the first element** of that block.
    
- Type: if `vector<int> v;` → `v.data()` is of type `int*`.
  
  

```
Syntax of the v.data():
```cpp
vector<int> v = {10, 20, 30};
int* ptr = v.data();   // ptr points to the first element of v

```

## **How it works**

- Now `ptr` behaves like a normal C-style array pointer:
```cpp
cout << ptr[0] << endl;  // 10
cout << ptr[1] << endl;  // 20
cout << ptr[2] << endl;  // 30

```

- You can also increment the pointer:
```cpp
 cout << *(ptr + 1) << endl; // 20

```

#### **Why use it?**

- Sometimes you need a **C-style array** for functions that don't accept vectors.
    
- `v.data()` gives you **direct access to the memory** without copying.
    

##### Example:

```cpp
#include <iostream>
#include <vector>
using namespace std;

void printArray(int* arr, int n) {
    for(int i=0; i<n; i++) cout << arr[i] << " ";
    cout << endl;
}

int main() {
    vector<int> v = {1, 2, 3, 4, 5};
    printArray(v.data(), v.size());  // pass vector as array
    return 0;
}

```

```ad-success
title: Output
1 2 3 4 5
```
### **Important Notes** 

1. `v.data()` points to **the internal array**, not a copy.
    
2. If the vector **resizes** after getting the pointer, the pointer may become invalid.
    
3. Useful for **interfacing with legacy C functions** that expect arrays.

#### Size and Capacity: 

|Function|Description|
|---|---|
|`size()`|Number of elements|
|`empty()`|True if vector is empty|
|`resize(n)`|Resize vector to n elements (new elements = 0/default)|
|`resize(n, val)`|Resize vector to n elements (new elements = val)|
|`capacity()`|Total allocated storage (may be larger than size)|
|`reserve(n)`|Preallocate memory for n elements|
|`shrink_to_fit()`|Reduce capacity to match size (release unused memory)|
|`max_size()`|Returns maximum possible size of vector|

```ad-info
title: Understanding Size vs Capacity
- **Size**: Number of elements currently in the vector
- **Capacity**: Amount of memory allocated (can hold elements without reallocation)
- Capacity is usually larger than size to avoid frequent reallocations
- Use `shrink_to_fit()` to free unused memory when capacity >> size
```

#### Other Useful Functions:

|Function|Description|Example|
|---|---|---|
|`assign(n, val)`|Assign n elements with value val|`v.assign(5, 10);`|
|`assign(first, last)`|Assign from iterator range|`v.assign(v2.begin(), v2.end());`|
|`swap(v2)`|Swap contents with another vector|`v1.swap(v2);`|

#### Example Code:

```cpp
#include <vector>
#include <iostream>

using namespace std;



int main()
{

	vector <int> vNumbers;


	vNumbers.push_back(10);

	vNumbers.push_back(20);

	vNumbers.push_back(30);

	vNumbers.push_back(40);

	vNumbers.push_back(50);



	cout << "First Element: " << vNumbers.front() << endl;

	cout << "Last Element: " << vNumbers.back() << endl;

	//returns the number of elements present in the vector
	cout << "Size: " << vNumbers.size() << endl;


	//check the overall size of a vector
	cout << "Capacity : " << vNumbers.capacity() << endl;


	//returns 1 (true) if the vector is empty
	cout << "Empty : " << vNumbers.empty() << endl;


	return 0;
}

```

#### Performance Tips:

```ad-success
title: Best Practices
1. **Use `reserve()`** if you know the approximate size beforehand to avoid multiple reallocations
2. **Use `emplace_back()`** instead of `push_back()` for complex objects
3. **Use `shrink_to_fit()`** to free memory after removing many elements
4. **Pass vectors by reference** to functions to avoid copying: `void func(vector<int>& v)`
5. **Use `const` reference** when not modifying: `void func(const vector<int>& v)`
```

#### Memory Management Example:

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;
    
    cout << "Initial capacity: " << v.capacity() << endl;
    
    // Reserve space for 100 elements
    v.reserve(100);
    cout << "After reserve(100): " << v.capacity() << endl;
    
    // Add 5 elements
    for(int i = 1; i <= 5; i++) {
        v.push_back(i);
    }
    
    cout << "Size: " << v.size() << endl;
    cout << "Capacity: " << v.capacity() << endl;
    
    // Shrink to fit actual size
    v.shrink_to_fit();
    cout << "After shrink_to_fit(): " << v.capacity() << endl;
    
    return 0;
}
```
