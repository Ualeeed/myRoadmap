---
DONE: true
DATE: 2025-08-23T00:04:00
---

## **1. What is a struct?**

A `struct` (short for structure) is a **user-defined data type** that groups variables together.

```c++

struct Student {
    string name;
    int age;
    float grade;
};

```


## **2. Vector of Structs**

- You can create a **vector that stores multiple structs**.
- Elements in a vector are stored contiguously in memory, allowing access through both iterators and pointer offsets.

```cpp

#include <iostream>
#include <vector>
using namespace std;

struct Student {
    string name;
    int age;
    float grade;
};

int main() {

    vector<Student> students;  // empty vector of Student structs
    
    return 0;
}


```

## **3. Adding Elements**

### Using `push_back()`

You can add elements using `push_back()`:

(a) With struct variable : 
```c++


Student s1;
s1.name = "Ali";
s1.age = 20;
s1.grade = 85.5;

students.push_back(s1);

```

(b) Using initializer list : 
```c++

students.push_back({"Sara", 19, 90.0});
students.push_back({"Waleed", 21, 88.5});

```

### Using `emplace_back()` (C++11 and later)

`emplace_back` is recommended when creating new temporary objects, while `push_back` is better when moving an existing object into the vector. In-place construction with `emplace_back` can be more performant than constructing and then moving the object.

```cpp
// Using emplace_back - constructs object directly in the vector
students.emplace_back("Ahmed", 22, 92.5);

// Equivalent to:
// Student temp = {"Ahmed", 22, 92.5};
// students.push_back(temp);
```

**Note:** Use `push_back` when you have an existing object to move, and use `emplace_back` when creating a new temporary object.

## **4. Accessing Elements**

### Important Safety Note
Always verify the vector is not empty and the index is valid when using the `[]` operator, as it does not add elements if none exist and causes undefined behavior with invalid indices.

```cpp
// Safe access with bounds checking
if (!students.empty() && index < students.size()) {
    cout << students[index].name << endl;
}

// Or use at() which throws exception on invalid index
try {
    cout << students.at(index).name << endl;
} catch (const out_of_range& e) {
    cout << "Invalid index!" << endl;
}
```

### Iterating Through Elements

You can use a **loop**: 
```cpp

for(int i = 0; i < students.size(); i++) {
    cout << "Name: " << students[i].name 
         << ", Age: " << students[i].age 
         << ", Grade: " << students[i].grade << endl;
}

```

Or **range-based for loop**: 
```cpp

for(auto s : students) {
    cout << s.name << " " << s.age << " " << s.grade << endl;
}

```

**Note:** Use `auto&` to avoid copying large structs:
```cpp
for(auto& s : students) {  // Reference avoids copying
    cout << s.name << " " << s.age << " " << s.grade << endl;
}
```


## **5. Full Example**

```cpp
#include <iostream>
#include <vector>
using namespace std;

struct Student {
    string name;
    int age;
    float grade;
};

int main() {
    vector<Student> students;

    students.push_back({"Ali", 20, 85.5});
    students.push_back({"Sara", 19, 90.0});
    students.push_back({"Waleed", 21, 88.5});

    cout << "Student List:" << endl;
    for(auto s : students) {
        cout << s.name << " | Age: " 
        << s.age << " | Grade: "
         << s.grade << endl;
    }

    return 0;
}

```

## **6. Extended Example with Functions**

```cpp
#include <vector>
#include <iostream>

using namespace std;



struct stEmployee
{
	string FirstName;
	string LastName;
	float Salary;
};


int main()
{


	// std::vector<T> vector_name;

	vector <stEmployee> vEmployees;

	stEmployee tempEmployee;


	tempEmployee.FirstName = "Ualid";

	tempEmployee.LastName = "Kurapika";

	tempEmployee.Salary = 5000;

	vEmployees.push_back(tempEmployee);


	tempEmployee.FirstName = "Ali";

	tempEmployee.LastName = "Maher";

	tempEmployee.Salary = 300;

	vEmployees.push_back(tempEmployee);



	tempEmployee.FirstName = "Aya";

	tempEmployee.LastName = "Omran";

	tempEmployee.Salary = 1000;

	vEmployees.push_back(tempEmployee);


	cout << "Employees Vector: \n\n";

	//ranged loop

	for (stEmployee & Employee : vEmployees) 
	{

		cout << "FirstName: " << Employee.FirstName << endl;

		cout << "LastName : " << Employee.LastName << endl;

		cout << "Salary : " << Employee.Salary << endl;

		cout << endl;

	}

	cout << endl;


	return 0;
}

```


## **7. Homework Solution**

```cpp
#include <vector>
#include <iostream>
using namespace std;



struct stEmployee
{
	string FirstName;
	string LastName;
	float Salary;
};


void ReadEmployees(vector <stEmployee> & vEmployees)
{

	char ReadMore = 'Y';

	stEmployee tempEmployee;

	while (ReadMore == 'Y' || ReadMore == 'y')
	{

		cout << "Enter FirstName? ";

		cin >> tempEmployee.FirstName;

		cout << "Enter LastName? ";

		cin >> tempEmployee.LastName;

		cout << "Enter Salary? ";

		cin >> tempEmployee.Salary;

		vEmployees.push_back(tempEmployee);

		cout << "\nDo you want to read more employees? Y/N ?";

		cin >> ReadMore;

	}
}

void PrintEmployees(vector <stEmployee> & vEmployees)
{

	cout << "\nEmployees Vector: \n\n";


	// ranged loop
	for (stEmployee & Employee : vEmployees) 
	{

		cout << "FirstName: " << Employee.FirstName << endl;
		cout << "LastName : " << Employee.LastName << endl;
		cout << "Salary : " << Employee.Salary << endl;
		cout << endl;
	}

	cout << endl;
}
int main()
{


	// std::vector<T> vector_name;

	vector <stEmployee> vEmployees;


	ReadEmployees(vEmployees);
	PrintEmployees(vEmployees);
	return 0;
}
```

## **8. Best Practices**

1. **Pass by Reference**: When passing vectors to functions, use reference parameters (`vector<T>&`) to avoid copying the entire vector.

2. **Reserve Capacity**: If you know the approximate size, use `reserve()` to prevent multiple reallocations:
   ```cpp
   vector<Student> students;
   students.reserve(100);  // Reserve space for 100 students
   ```

3. **Check Bounds**: Always validate indices before accessing elements with `[]` operator, or use `at()` for automatic bounds checking.

4. **Use Auto with References**: When iterating, use `auto&` instead of `auto` to avoid unnecessary copying of struct objects.

5. **Choose Right Method**: Use `emplace_back()` for constructing objects in place, and `push_back()` when you already have an object to move.

6. **Memory Management**: Vectors handle memory automatically - you don't need to manually deallocate memory.
