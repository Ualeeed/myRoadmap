---
DONE: true
DATE: 2025-08-22T16:50:00
---



#### **Input validation**
*is the process of checking whether user input conforms to what the program is expecting. A program that handles error cases well is said to be robust.

### Types of Invalid Input

There are four main types of input errors to handle:

1. **Extraction succeeds but input is meaningless** (e.g., entering 'k' for a mathematical operator)
2. **Extraction succeeds but user enters additional input** (e.g., entering '*q hello' for an operator)
3. **Extraction fails** (e.g., trying to enter 'q' into a numeric variable)
4. **Extraction succeeds but user overflows a numeric value**

### Basic Validation Example

```cpp
#include <iostream>
#include <limits>
using namespace std;

int ReadNumber()
{
	int Number;

	cout << "Please enter a number?" << endl;
	cin >> Number;

	while (cin.fail()) 
	{
		// user didn't input a number
		cin.clear();
		cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
		
		cout << "Invalid Number, Enter a valid one:" << endl;
		cin >> Number;
	}

	return Number;
}

int main()
{
	cout << "Your Number is:" << ReadNumber();
	return 0;
}
```

### Helper Functions for Robust Input Validation

#### 1. Ignore Line Function
```cpp
#include <limits>

void ignoreLine()
{
	std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
}
```

This function removes all characters from the input buffer up to and including the newline character.

#### 2. Clear Failed Extraction Function
```cpp
#include <cstdlib>

// returns true if extraction failed, false otherwise
bool clearFailedExtraction()
{
	if (!std::cin) // If the previous extraction failed
	{
		if (std::cin.eof()) // If the stream was closed (EOF)
		{
			std::exit(0); // Shut down the program
		}
		
		std::cin.clear(); // Put us back in 'normal' operation mode
		ignoreLine(); // Remove the bad input
		return true;
	}
	return false;
}
```

#### 3. Check for Unextracted Input
```cpp
// returns true if std::cin has unextracted input on the current line
bool hasUnextractedInput()
{
	return !std::cin.eof() && std::cin.peek() != '\n';
}
```

### Complete Validation Example with Error Handling

```cpp
#include <iostream>
#include <limits>
#include <cstdlib>

void ignoreLine()
{
	std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
}

bool clearFailedExtraction()
{
	if (!std::cin)
	{
		if (std::cin.eof())
		{
			std::exit(0);
		}
		std::cin.clear();
		ignoreLine();
		return true;
	}
	return false;
}

double getDouble()
{
	while (true) // Loop until user enters valid input
	{
		std::cout << "Enter a decimal number: ";
		double x{};
		std::cin >> x;
		
		if (clearFailedExtraction())
		{
			std::cout << "Invalid input. Please try again.\n";
			continue;
		}
		
		ignoreLine(); // Remove any extraneous input
		return x;
	}
}

char getOperator()
{
	while (true)
	{
		std::cout << "Enter one of the following: +, -, *, or /: ";
		char operation{};
		std::cin >> operation;
		
		if (!clearFailedExtraction())
			ignoreLine();
		
		switch (operation)
		{
			case '+':
			case '-':
			case '*':
			case '/':
				return operation;
			default:
				std::cout << "Invalid operator. Please try again.\n";
		}
	}
}

int main()
{
	double x = getDouble();
	char operation = getOperator();
	double y = getDouble();
	
	// Handle division by zero
	while (operation == '/' && y == 0.0)
	{
		std::cout << "Cannot divide by zero. Enter another number: ";
		y = getDouble();
	}
	
	std::cout << x << ' ' << operation << ' ' << y << " = ";
	
	switch (operation)
	{
		case '+': std::cout << x + y << '\n'; break;
		case '-': std::cout << x - y << '\n'; break;
		case '*': std::cout << x * y << '\n'; break;
		case '/': std::cout << x / y << '\n'; break;
	}
	
	return 0;
}
```

### Key Validation Principles

1. **Always check if extraction succeeded** using `if (!std::cin)` or `if (std::cin.fail())`
2. **Clear the error state** with `std::cin.clear()` after a failed extraction
3. **Remove bad input** from the buffer using `ignoreLine()`
4. **Use loops** to repeatedly ask for input until valid data is received
5. **Validate meaning** - even if extraction succeeds, check if the input makes sense for your program
6. **Handle EOF** - detect when user enters end-of-file character (Ctrl+D on Unix, Ctrl+Z on Windows)

### Best Practices

- Always validate numeric input to ensure it's of the correct type and within expected ranges
- For each point of input, consider: Could extraction fail? Could the user enter more than expected? Could the input be meaningless? Could overflow occur?
- Make your programs robust by anticipating how users might misuse them
- Use meaningful error messages to guide users toward correct input