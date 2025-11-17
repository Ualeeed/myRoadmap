---
DONE: true
DATE: 2025-08-22T23:47:00
---

#### **Using `push_back()`**

Adds an element **at the end** of the vector.

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> vNumber;

    vNumber.push_back(10);  // v = {10}
    vNumber.push_back(20);  // v = {10, 20}
    vNumber.push_back(30);  // v = {10, 20, 30}

    for(int& Number : vNumber) 
	    cout << Number << " ";
    
    return 0;
}

```

**Key Points about `push_back()`:**
- Automatically resizes the vector if there is not enough space to accommodate the new element
- If after the operation the new size() is greater than old capacity() a reallocation takes place, in which case all iterators (including the end() iterator) and all references to the elements are invalidated
- Time Complexity: Constant (amortized time)
- Creates a copy or moves the element into the vector


### Using `insert()` : 

Lets you insert an element **at any position**.

```cpp
vector<int> vNumber = {1, 2, 4};

vNumber.insert(vNumber.begin() + 2, 3);   // insert 3 at index 2
// v = {1, 2, 3, 4}

```

**Key Points about `insert()`:**
- Returns an iterator to the inserted element. All the elements to the right of the given index will be shifted once place to the right to make space for new element
- Can insert at any position in the vector
- More flexible but potentially slower than `push_back()` for end insertions

#### Adding Multiple Elements : 

```cpp
vector<int> vNumber = {1, 2};
vNumber.insert(vNumber.end(), {3, 4, 5});   // add at the end
// v = {1, 2, 3, 4, 5}

```


# **Difference between `push_back` and `insert`**

- `push_back(x)` → always adds at the end.
    
- `insert(pos, x)` → adds at a specific position.

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<string> names;

    names.push_back("Ali");
    names.push_back("Sara");
    names.insert(names.begin(), "Waleed"); // at start

    for(string& n : names)
	     cout << n << " ";
	     
    return 0;
}

```

Output: 

```ad-success
title: Outout
Waleed Ali Sara


```

---

## **Advanced: `emplace_back()` (C++11 and later)**

`emplace_back()` is a more efficient alternative to `push_back()` introduced in C++11.

**Key Differences:**
- emplace_back() constructs the object in the containers storage directly, while `push_back()` creates a temporary object and then moves it
- emplace_back performs explicit conversions and directly constructs elements in place without creating temporaries
- Generally more performant when creating new objects

**When to Use:**
- Use push_back when you have an existing temporary object that you want to move into your vector. Use emplace_back when you create a new temporary object

**Example:**
```cpp
#include <iostream>
#include <vector>
using namespace std;

class Person {
public:
    string name;
    int age;
    
    Person(string n, int a) : name(n), age(a) {
        cout << "Constructor called for " << name << endl;
    }
};

int main() {
    vector<Person> people;
    
    // push_back: creates temporary then moves
    people.push_back(Person("Ali", 25));
    
    // emplace_back: constructs directly in vector (more efficient)
    people.emplace_back("Sara", 30);
    
    return 0;
}
```

---

## **Examples from Practice:**

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


	cout << "Numbers Vector: \n\n";

	// ranged loop

	for (int& Number : vNumbers)
	{

		cout << Number << endl;

	}


	cout << endl;

	return 0;
 }

```


-  Homework Solution

```cpp
#include <vector>
#include <iostream>

using namespace std;



void ReadNumbers(vector <int> & vNumbers)
{

	char ReadMore = 'Y';

	int Number;


	while (ReadMore == 'Y' || ReadMore == 'y')
	{

		cout << "Please enter a number? ";
		cin >> Number;

		vNumbers.push_back(Number);

		cout << "\nDo you want to read more numbers? Y/N ?";
		cin >> ReadMore;

	}

}


void PrintVectorNumbers(vector <int>& vNumbers)
{

	cout << "Numbers Vector: \n\n";


	// ranged loop
	for (int & Number : vNumbers)
	{
		cout << Number << endl;
	}
	cout << endl;
}

int main()
{


	vector <int> vNumbers;


	ReadNumbers(vNumbers);


	PrintVectorNumbers(vNumbers);



	return 0;
 }

```

---

## **Performance Summary**

| Method | Position | Performance | Best Use Case |
|--------|----------|-------------|---------------|
| `push_back()` | End only | Good (amortized O(1)) | Adding existing objects to end |
| `emplace_back()` | End only | Better (amortized O(1)) | Creating new objects at end |
| `insert()` | Any position | Slower (O(n)) | Inserting at specific positions |

**Note:** For most simple cases with basic types (int, double, etc.), the performance difference between `push_back()` and `emplace_back()` is negligible. The advantage becomes more apparent with complex objects.
