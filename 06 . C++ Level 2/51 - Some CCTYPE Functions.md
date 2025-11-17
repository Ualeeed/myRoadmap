---
DONE: true
DATE: 2025-08-23T08:31:00
---


```cpp
#include <iostream>
#include <string>
#include <cctype>

using namespace std;


int main()
{

	char x;

	char w;

	x = toupper('a');

	w = tolower('A');

	cout << "converting a to A: " << x << endl;

	cout << "converting A to a: " << w << endl;


	// Digits (A to Z)
	// returns zero if not, and non zero of yes

	cout << "isupper('A') " << isupper('A') << endl;

	// lower case (a to z)
	// returns zero if not, and non zero of yes

	cout << "islower('A') " << islower('A') << endl;

	// Digits (0 to 9)
	// returns zero if not, and non zero of yes

	cout << "isdigit('A') " << isdigit('A') << endl;

	// punctuation characters are !"#$%&'()*+,-./:;<=>?@[\]^_`{|}~
	// returns zero if not, and non zero of yes

	cout << "ispunct('A') " << ispunct('A') << endl;


	return 0;
}

```


|Function|Description|Example|Returns|
|---|---|---|---|
|`toupper(ch)`|Converts a lowercase letter to uppercase|`toupper('a')` → `'A'`|char|
|`tolower(ch)`|Converts an uppercase letter to lowercase|`tolower('A')` → `'a'`|char|
|`isupper(ch)`|Checks if the character is uppercase (A–Z)|`isupper('A')` → 1|int|
|`islower(ch)`|Checks if the character is lowercase (a–z)|`islower('A')` → 0|int|
|`isdigit(ch)`|Checks if the character is a digit (0–9)|`isdigit('A')` → 0|int|
|`ispunct(ch)`|Checks if the character is a punctuation mark|`ispunct('A')` → 0|int|
**Note:** Functions like `isupper()`, `islower()`, `isdigit()`, and `ispunct()` return **non-zero (true)** if the condition is met, otherwise **0 (false)**.

   - Space (' ')
   - Tab ('\\t')
   - Newline ('\\n')
   - Carriage return `('\\r')`
   - Form feed `('\\f')`
   - Vertical tab `('\\v')` 

10. **Punctuation Includes:** `!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~`
 
---

