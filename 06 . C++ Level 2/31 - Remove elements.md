---
DONE: true
DATE: 2025-08-23T00:30:00
---

# Removing Elements from C++ Vectors

There are several methods to remove elements from a vector in C++. Each method serves different purposes and has different performance characteristics.

---

## **1. pop_back() - Remove Last Element**

### What is `pop_back()`?

- `pop_back()` **removes the last element** from a vector.
- It **does not return the element** (unlike some other languages).
- The **size of the vector decreases by 1**.
- **Time Complexity**: O(1) - constant time operation.

### Example:

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
	
	// LIFO : Last_In_First_Out

	vNumbers.pop_back(); // delete 50
	vNumbers.pop_back(); // delete 40
	vNumbers.pop_back(); // delete 30
	vNumbers.pop_back(); // delete 20
	vNumbers.pop_back(); // delete 10 

	cout << "Numbers Vector: \n\n";

	// ranged loop
	for (int & Number : vNumbers) 
	{
		cout << Number << endl;
	}
	cout << endl;

	return 0;
}
```

### Important Notes:

- `pop_back()` **only removes the last element**.
- Calling `pop_back()` on an **empty vector** leads to **undefined behavior** → always check size first.

#### Safe Usage:
```c++
if(!v.empty()) {
    v.pop_back();
}
```

---

## **2. erase() - Remove Element(s) at Specific Position**

The `erase()` method removes one element at a specific position or a range of elements using iterators.

### Syntax:

```cpp
// Remove single element
vector.erase(iterator position);

// Remove range of elements
vector.erase(iterator first, iterator last);
```

### Examples:

#### Remove Single Element:
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> numbers = {10, 20, 30, 40, 50};
    
    // Remove element at index 2 (value 30)
    numbers.erase(numbers.begin() + 2);
    
    // Output: 10 20 40 50
    for(int num : numbers) {
        cout << num << " ";
    }
    
    return 0;
}
```

#### Remove Range of Elements:
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> numbers = {10, 20, 30, 40, 50, 60};
    
    // Remove elements from index 1 to 3 (20, 30, 40)
    numbers.erase(numbers.begin() + 1, numbers.begin() + 4);
    
    // Output: 10 50 60
    for(int num : numbers) {
        cout << num << " ";
    }
    
    return 0;
}
```

#### Remove First Element:
```cpp
vector<int> numbers = {10, 20, 30, 40, 50};
numbers.erase(numbers.begin());  // Removes 10
```

#### Remove Last Element (Alternative to pop_back):
```cpp
vector<int> numbers = {10, 20, 30, 40, 50};
numbers.erase(numbers.end() - 1);  // Removes 50
```

### Performance Considerations:

Erasing from the end of the vector is constant time, but erasing from the beginning or middle requires linear time because all subsequent elements must be shifted.

- **End removal**: O(1)
- **Beginning/Middle removal**: O(n)

### Important Notes:

Iterators and references at or after the erase point are invalidated after the operation.

```cpp
// ⚠️ WRONG - Iterator invalidation
for(auto it = vec.begin(); it != vec.end(); it++) {
    if(*it == valueToRemove) {
        vec.erase(it);  // it is now invalid!
    }
}

// ✅ CORRECT - Update iterator
for(auto it = vec.begin(); it != vec.end(); ) {
    if(*it == valueToRemove) {
        it = vec.erase(it);  // erase returns next valid iterator
    } else {
        ++it;
    }
}
```

---

## **3. clear() - Remove All Elements**

The `clear()` method removes all elements from the vector, leaving it with a size of zero.

### Example:

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> numbers = {10, 20, 30, 40, 50};
    
    cout << "Size before: " << numbers.size() << endl;  // 5
    
    numbers.clear();
    
    cout << "Size after: " << numbers.size() << endl;   // 0
    
    return 0;
}
```

### Notes:
- **Time Complexity**: O(n)
- The capacity of the vector remains unchanged
- To free memory, use `shrink_to_fit()` after `clear()`:

```c++
numbers.clear();
numbers.shrink_to_fit();  // Release unused memory
```

---

## **4. Erase-Remove Idiom - Remove Elements by Value**

When removing multiple elements, calling erase repeatedly generates overhead from repeatedly moving elements. The erase-remove idiom is a more efficient technique.

### The Problem:
```cpp
// ❌ Inefficient - multiple shifts
vector<int> vec = {1, 2, 3, 2, 4, 2, 5};
for(auto it = vec.begin(); it != vec.end(); ) {
    if(*it == 2) {
        it = vec.erase(it);  // Shifts all following elements
    } else {
        ++it;
    }
}
```

### The Solution - Erase-Remove Idiom:

The remove algorithm returns an iterator to the beginning of unused elements, then erase can eliminate them efficiently.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> vec = {1, 2, 3, 2, 4, 2, 5};
    
    // Remove all occurrences of value 2
    vec.erase(remove(vec.begin(), vec.end(), 2), vec.end());
    
    // Output: 1 3 4 5
    for(int num : vec) {
        cout << num << " ";
    }
    
    return 0;
}
```

### How It Works:

1. `std::remove()` moves elements to keep to the front
2. Returns iterator to new "logical end"
3. `erase()` removes the "garbage" elements at the end

### Remove with Condition (remove_if):

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> vec = {1, 2, 3, 4, 5, 6, 7, 8, 9};
    
    // Remove all odd numbers
    vec.erase(
        remove_if(vec.begin(), vec.end(), 
                  [](int x) { return x % 2 != 0; }),
        vec.end()
    );
    
    // Output: 2 4 6 8
    for(int num : vec) {
        cout << num << " ";
    }
    
    return 0;
}
```

### Why Use Erase-Remove Idiom?

When removing multiple elements, remove copies each kept element only once to its final location, whereas repeated erase calls would shift elements multiple times.

---

## **5. Comparison of Methods**

| Method | Use Case | Time Complexity | Notes |
|--------|----------|----------------|-------|
| `pop_back()` | Remove last element | O(1) | Fastest, but only for last element |
| `erase(pos)` | Remove at specific position | O(n) | Simple but shifts elements |
| `erase(first, last)` | Remove range | O(n) | Efficient for removing a range |
| `clear()` | Remove all elements | O(n) | Keeps capacity |
| Erase-Remove | Remove by value/condition | O(n) | Most efficient for multiple removals |

---

## **6. Best Practices**

1. **Check Before Removing**: Always verify the vector is not empty before using `pop_back()`.

2. **Handle Iterator Invalidation**: When using `erase()` in a loop, update the iterator properly.

3. **Use Erase-Remove for Multiple Elements**: The erase-remove idiom is highly efficient for removing multiple items in a single pass.

4. **Consider Alternative Data Structures**: If you frequently remove elements from the beginning or middle, consider using `std::list` or `std::deque`.

5. **Reserve Capacity**: If you know the approximate final size, use `reserve()` to minimize reallocations.

6. **Use `shrink_to_fit()`**: After removing many elements, call `shrink_to_fit()` to release unused memory.

---

## **7. Complete Example - All Methods**

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

void printVector(const vector<int>& v, const string& label) {
    cout << label << ": ";
    for(int num : v) {
        cout << num << " ";
    }
    cout << endl;
}

int main() {
    // 1. Using pop_back()
    vector<int> v1 = {1, 2, 3, 4, 5};
    v1.pop_back();
    printVector(v1, "After pop_back()");  // 1 2 3 4
    
    // 2. Using erase() - single element
    vector<int> v2 = {1, 2, 3, 4, 5};
    v2.erase(v2.begin() + 2);  // Remove element at index 2
    printVector(v2, "After erase(index 2)");  // 1 2 4 5
    
    // 3. Using erase() - range
    vector<int> v3 = {1, 2, 3, 4, 5};
    v3.erase(v3.begin() + 1, v3.begin() + 4);  // Remove indices 1-3
    printVector(v3, "After erase(range 1-3)");  // 1 5
    
    // 4. Using clear()
    vector<int> v4 = {1, 2, 3, 4, 5};
    v4.clear();
    cout << "After clear(), size: " << v4.size() << endl;  // 0
    
    // 5. Using erase-remove idiom
    vector<int> v5 = {1, 2, 3, 2, 4, 2, 5};
    v5.erase(remove(v5.begin(), v5.end(), 2), v5.end());
    printVector(v5, "After erase-remove (value 2)");  // 1 3 4 5
    
    // 6. Using erase-remove_if idiom
    vector<int> v6 = {1, 2, 3, 4, 5, 6, 7, 8, 9};
    v6.erase(remove_if(v6.begin(), v6.end(), 
             [](int x) { return x % 2 != 0; }), v6.end());
    printVector(v6, "After remove_if (odd numbers)");  // 2 4 6 8
    
    return 0;
}
```

---

## **Summary**

- Use **`pop_back()`** for quick removal of the last element
- Use **`erase()`** for removing specific positioned elements
- Use **`clear()`** to remove all elements
- Use **erase-remove idiom** for efficient removal of elements by value or condition
- Always handle iterator invalidation when using `erase()` in loops
- Consider performance implications when removing from the middle of large vectors