---
DONE: true
DATE: 2025-08-23T16:35:00
---



```c++
#pragma warning(disable : 4996)

#include <ctime>
#include <iostream>

using namespace std;


int main()
{

	time_t t = time(0); // get time now

	char* dt = ctime(&t); // convert in string form

	cout << "Local date and time is: " << dt << "\n";

	// converting now to tm struct for UTC date/time

	tm* gmtm = gmtime(&t);

	dt = asctime(gmtm);

	cout << "UTC date and time is: " << dt;

	return 0;
}

```

#### Breakdown the code : 


```cpp
#pragma warning(disable : 4996)
```

- This is for **Visual Studio (MSVC)**.
    
- Functions like `ctime`, `asctime`, `gmtime` are considered _unsafe_ in MSVC because they return pointers to internal static buffers.
    
- Without this line, you’d get a warning: _“This function or variable may be unsafe”_.
    
- This directive disables that warning.


```cpp
#include <ctime>
#include <iostream>

using namespace std;
```

- `<ctime>` → contains time-related functions (`time`, `ctime`, `gmtime`, `asctime`).
    
- `<iostream>` → for input/output (`cout`).


```cpp
time_t t = time(0); // get time now
```

- `time_t` → a data type that stores **time in seconds since Jan 1, 1970 (Unix epoch)**.
    
- `time(0)` → gets the current system time.


```cpp
char* dt = ctime(&t); // convert in string form
cout << "Local date and time is: " << dt << "\n";
```

- `ctime(&t)` → converts `time_t` into a **human-readable local time string**.
    
- Example output:

```sql
Local date and time is: Sat Aug 23 16:25:45 2025
```


```cpp
tm* gmtm = gmtime(&t);
dt = asctime(gmtm);
cout << "UTC date and time is: " << dt;
```

- `gmtime(&t)` → converts `time_t` into a `tm` structure in **UTC (Greenwich Mean Time)**.
    
- `asctime(gmtm)` → converts the `tm` structure into a readable string.
    
- Example output:

```sql
UTC date and time is: Sat Aug 23 15:25:45 2025
```

