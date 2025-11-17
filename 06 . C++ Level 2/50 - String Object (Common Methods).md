---
DONE: true
DATE: 2025-08-23T08:29:00
---


The `std::string` class in C++ provides a rich set of methods for string manipulation. This guide covers the most commonly used methods organized by functionality.

---

## 📏 Size and Capacity Methods

| Method | Description | Example | Return Type |
|--------|-------------|---------|-------------|
| `length()` | Returns number of characters | `s.length()` | `size_t` |
| `size()` | Same as `length()` | `s.size()` | `size_t` |
| `empty()` | Checks if string is empty | `s.empty()` | `bool` |
| `capacity()` | Returns allocated storage capacity | `s.capacity()` | `size_t` |
| `max_size()` | Returns maximum possible size | `s.max_size()` | `size_t` |
| `reserve(n)` | Requests capacity change | `s.reserve(100)` | `void` |
| `shrink_to_fit()` | Reduces capacity to fit size | `s.shrink_to_fit()` | `void` |

---

## 🔍 Element Access Methods

| Method | Description | Example | Notes |
|--------|-------------|---------|-------|
| `at(index)` | Returns character at index (with bounds checking) | `s.at(0)` | Throws `out_of_range` exception |
| `operator[]` | Returns character at index (no bounds checking) | `s[0]` | Undefined behavior if out of range |
| `front()` | Returns first character | `s.front()` | C++11, undefined if empty |
| `back()` | Returns last character | `s.back()` | C++11, undefined if empty |
| `c_str()` | Returns C-style null-terminated string | `s.c_str()` | Returns `const char*` |
| `data()` | Returns pointer to string data | `s.data()` | Returns `const char*` |

---

## ➕ Modifying Methods

### Adding Content

| Method | Description | Example | Notes |
|--------|-------------|---------|-------|
| `append(str)` | Appends string to end | `s.append(" World")` | Can append multiple types |
| `push_back(ch)` | Adds single character at end | `s.push_back('!')` | Single character only |
| `operator+=` | Appends string or character | `s += "text"` | Convenient shorthand |
| `insert(pos, str)` | Inserts string at position | `s.insert(5, "Hi")` | Multiple overloads available |

### Removing Content

| Method | Description | Example | Notes |
|--------|-------------|---------|-------|
| `erase(pos, len)` | Erases characters from position | `s.erase(5, 3)` | If `len` omitted, erases to end |
| `pop_back()` | Removes last character | `s.pop_back()` | C++11, undefined if empty |
| `clear()` | Removes all characters | `s.clear()` | Size becomes 0 |

### Replacing Content

| Method | Description | Example | Notes |
|--------|-------------|---------|-------|
| `replace(pos, len, str)` | Replaces substring | `s.replace(0, 5, "Hi")` | Multiple overloads |
| `assign(str)` | Assigns new content | `s.assign("New text")` | Replaces entire string |

---

## 🔎 Search Methods

| Method | Description | Example | Return Value |
|--------|-------------|---------|--------------|
| `find(str)` | Finds first occurrence | `s.find("text")` | Position or `npos` |
| `rfind(str)` | Finds last occurrence | `s.rfind("text")` | Position or `npos` |
| `find_first_of(str)` | Finds first char matching any in str | `s.find_first_of("aeiou")` | Position or `npos` |
| `find_last_of(str)` | Finds last char matching any in str | `s.find_last_of("aeiou")` | Position or `npos` |
| `find_first_not_of(str)` | Finds first char NOT in str | `s.find_first_not_of(" ")` | Position or `npos` |
| `find_last_not_of(str)` | Finds last char NOT in str | `s.find_last_not_of(" ")` | Position or `npos` |

**Note:** `string::npos` is a special constant (usually -1 or max value) indicating "not found"

---

##  String Operations

| Method | Description | Example | Return Type |
|--------|-------------|---------|-------------|
| `substr(pos, len)` | Extracts substring | `s.substr(0, 5)` | `string` |
| `compare(str)` | Compares strings lexicographically | `s.compare("abc")` | `int` (0 if equal) |
| `swap(str)` | Swaps content with another string | `s1.swap(s2)` | `void` |
| `resize(n)` | Resizes string to n characters | `s.resize(10)` | `void` |
| `copy(buffer, len, pos)` | Copies substring to character array | `s.copy(buf, 5, 0)` | `size_t` |

---

## 📝 Practical Example

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string S1 = "My Name is Ualid , I LoveProgramming.";

    // Size and capacity methods
    cout << "Length: " << S1.length() << endl;
    cout << "Is empty? " << (S1.empty() ? "Yes" : "No") << endl;
    
    // Element access
    cout << "Character at index 3: " << S1.at(3) << endl;
    cout << "First character: " << S1.front() << endl;
    cout << "Last character: " << S1.back() << endl;
    
    // Modifying content - append
    S1.append(" @ProgrammingAdvices");
    cout << "After append: " << S1 << endl;
    
    // Insert
    S1.insert(17, " ah ");
    cout << "After insert: " << S1 << endl;
    
    // Substring
    cout << "Substring (16, 8): " << S1.substr(16, 8) << endl;
    
    // Push back and pop back
    S1.push_back('X');
    cout << "After push_back: " << S1 << endl;
    
    S1.pop_back();
    cout << "After pop_back: " << S1 << endl;
    
    // Finding text
    cout << "Position of 'ah': " << S1.find("ah") << endl;
    cout << "Position of 'Ah': " << S1.find("Ah") << endl;
    
    // Check if substring not found
    if (S1.find("Ah") == string::npos)
    {
        cout << "'Ah' is not found" << endl;
    }
    
    // Erase part of string
    S1.erase(0, 10);
    cout << "After erase: " << S1 << endl;
    
    // Replace
    string S2 = "Hello World";
    S2.replace(6, 5, "C++");
    cout << "After replace: " << S2 << endl;
    
    // Compare
    string S3 = "abc";
    string S4 = "abc";
    if (S3.compare(S4) == 0)
    {
        cout << "S3 and S4 are equal" << endl;
    }
    
    // Clear
    S1.clear();
    cout << "After clear, length: " << S1.length() << endl;

    return 0;
}
```

---

##  Important Notes

1. **String Index:** Strings in C++ are 0-indexed (first character is at index 0)
2. **Bounds Checking:** Use `at()` for safe access with bounds checking, or `[]` for faster access without bounds checking
3. **Case Sensitivity:** All search operations are case-sensitive
4. **Return Value:** Most find operations return `string::npos` when not found
5. **Efficiency:** Use `reserve()` to pre-allocate memory if you know the approximate final size
6. **C-Style Strings:** Use `c_str()` when interfacing with C libraries that require `char*`
7. **Iterator Support:** Strings support iterators via `begin()`, `end()`, `rbegin()`, `rend()` for use with STL algorithms

---
