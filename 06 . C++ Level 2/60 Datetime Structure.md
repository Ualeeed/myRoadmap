---
DONE: true
DATE: 2025-08-23T16:41:00
---



```cpp

#pragma warning(disable : 4996)
#include <ctime>
#include <iostream>
using namespace std;
/*
int tm_sec; // seconds of minutes from 0 to 61
int tm_min; // minutes of hour from 0 to 59
int tm_hour; // hours of day from 0 to 24
int tm_mday; // day of month from 1 to 31
int tm_mon; // month of year from 0 to 11
int tm_year; // year since 1900
int tm_wday; // days since sunday
int tm_yday; // days since January 1st
int tm_isdst; // hours of daylight savings time
*/
int main() {
time_t t = time(0); // get time now
tm* now = localtime(&t);
cout << "Year: " << now->tm_year + 1900 << endl;
cout << "Month: " << now->tm_mon + 1 << endl;
cout << "Day: " << now->tm_mday << endl;
cout << "Hour: " << now->tm_hour << endl;
cout << "Min: " << now->tm_min << endl;
cout << "Second: " << now->tm_sec << endl;
cout << "Week Day (Days since sunday): " << now->tm_wday << endl;
cout << "Year Day (Days since Jan 1st): " << now->tm_yday << endl;
cout << "hours of daylight savings:" << now->tm_isdst << endl;
}

```


## Code Explanation

```cpp
time_t t = time(0); // get current time in seconds since 1970 tm* now = localtime(&t); // convert to local time components
```

- `time_t t` stores the current time in **epoch seconds**.
    
- `localtime(&t)` converts `t` into a `tm` struct with detailed date/time info.
    
- `now` is a pointer → to access fields, you use `now->tm_hour`, `now->tm_min`, etc.
    

---

### 🔹 Breakdown of Printed Values

1. **Year**
```cpp
 cout << "Year: " << now->tm_year + 1900 << endl;
```
    
    - tm_year = years since 1900 → must add 1900.
        
    - Example: if `tm_year = 125`, it means 2025.
        
2. **Month**
    
```cpp
cout << "Month: " << now->tm_mon + 1 << endl;
```
    
    - tm_mon = 0–11 → add 1 to get 1–12.
        
    - Example: 7 = August.
        
3. **Day of Month**
    
```cpp
cout << "Day: " << now->tm_mday << endl;
```
    
    - Range: 1–31.
        
4. **Hour / Minute / Second**
    
```cpp
`cout << "Hour: " << now->tm_hour << endl; cout << "Min: " << now->tm_min << endl; cout << "Second: " << now->tm_sec << endl;`
```
    
    - tm_hour: 0–23 (24-hour format).
        
    - tm_min: 0–59.
        
    - tm_sec: 0–60 (leap seconds possible).
        
5. **Weekday**
    
```cpp
cout << "Week Day (Days since sunday): " << now->tm_wday << endl;
```
    
    - 0 = Sunday, 1 = Monday, …, 6 = Saturday.
        
6. **Year Day**
    
```cpp
cout << "Year Day (Days since Jan 1st): " << now->tm_yday << endl;
```
    
    - Range: 0–365.
        
    - Example: Aug 23 = 234.
        
7. **Daylight Saving**
    
```cpp
cout << "hours of daylight savings:" << now->tm_isdst << endl;
```
    
    - > 0 → Daylight Saving Time in effect.
        
    - 0 → No DST.
        
    - < 0 → Unknown.