---
DONE: true
DATE: 2025-08-23
---


-  Swap Using Reference

```cpp
#include <iostream>

using namespace std;

void swap(int& n1, int& n2)
{
	int temp;
	temp = n1;
	n1 = n2;
	n2 = temp;
}


int main()
{

	int a = 1, b = 2;

	cout << "Before swapping" << endl;

	cout << "a = " << a << endl;

	cout << "b = " << b << endl;


	swap(a, b);


	cout << "\nAfter swapping" << endl;

	cout << "a = " << a << endl;

	cout << "b = " << b << endl;


	return 0;
}

```

- Parameters `int& n1` and `int& n2` are **references (aliases)** to the original variables.
    
- When you call:
```c++
swap(a, b);
```

- `n1` becomes another name for `a`.
    
- `n2` becomes another name for `b`.

So when you modify `n1` or `n2`, you’re directly modifying `a` and `b`.


#### Swap Using Pointers:

```cpp
#include <iostream>

using namespace std;

void swap(int* n1, int* n2)
{
	int temp;
	temp = *n1;
	*n1 = *n2;
	*n2 = temp;
}
int main()
{

	int a = 1, b = 2;

	cout << "Before swapping" << endl;

	cout << "a = " << a << endl;

	cout << "b = " << b << endl;


	swap(&a, &b);

	cout << "\nAfter swapping" << endl;

	cout << "a = " << a << endl;

	cout << "b = " << b << endl;


	return 0;
}

```

- Parameters `int* n1` and `int* n2` are **pointers** (they store addresses of variables).
    
- You call the function with:
```c++
swap(&a, &b);
```

- `n1` stores the address of `a`.
    
- `n2` stores the address of `b`.

Inside the function:

- `*n1` means "go to address stored in `n1` and get/change the value of `a`".
    
- `*n2` does the same for `b`.

| Feature             | Using References                  | Using Pointers                  |
| ------------------- | --------------------------------- | ------------------------------- |
| Function definition | `void swap(int& n1, int& n2)`     | `void swap(int* n1, int* n2)`   |
| Function call       | `swap(a, b);`                     | `swap(&a, &b);`                 |
| Inside function     | Use `n1`, `n2` directly           | Must dereference `*n1`, `*n2`   |
| Safety              | Always refers to a valid variable | Can be `nullptr` (dangerous)    |
| Readability         | Cleaner, easier                   | More verbose, but more flexible |