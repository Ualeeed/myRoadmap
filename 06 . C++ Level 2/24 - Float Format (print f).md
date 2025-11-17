---
DONE: true
DATE: 2025-09-26T12:00:00
---

## **1. Basic Float Specifiers**

| Specifier | Meaning                                                     | Example (`float x = 123.456;`) |
| --------- | ----------------------------------------------------------- | ------------------------------ |
| `%f`      | Fixed-point decimal (default 6 decimal places)              | `123.456000`                   |
| `%F`      | Same as `%f` but uppercase for special values (INF, NAN)    | `123.456000`                   |
| `%e`      | Scientific notation (lowercase `e`)                         | `1.234560e+02`                 |
| `%E`      | Scientific notation (uppercase `E`)                         | `1.234560E+02`                 |
| `%g`      | Uses `%f` or `%e` (whichever is shorter, no trailing zeros) | `123.456`                      |
| `%G`      | Same as `%g` but with uppercase `E` if scientific           | `123.456`                      |

## **2. Precision Control**

### **Fixed Precision**
- `%.3f` - Exactly 3 decimal places
- `%.0f` - No decimal places (rounds to nearest integer)
- Default precision for `%f` is 6 decimal places

### **Dynamic Precision**
- `%.*f` - Precision specified by an additional integer argument
- The precision argument comes **before** the float value

### **Lossless Printing**
For printing floating-point numbers that can be read back exactly (round-trip conversion):
- **float**: Use `printf("%.9g", number)`
- **double**: Use `printf("%.17g", number)`

## **3. Width and Padding**

### **Field Width**
- `%10f` - Minimum 10 characters wide, right-aligned
- `%-10f` - Minimum 10 characters wide, left-aligned
- `%010f` - Minimum 10 characters, padded with leading zeros (except for infinity or NaN)

### **Combined Width and Precision**
- `%10.3f` - 10 characters wide, 3 decimal places
- `%*.*f` - Both width and precision from arguments

## **4. Special Values Handling**

Floating-point special values are formatted as follows:
- **Infinity**: `inf` (lowercase specifiers) or `INF` (uppercase specifiers)
- **NaN**: `nan` (lowercase specifiers) or `NAN` (uppercase specifiers)

## **5. Type Specifiers for Different Float Types**

| Type                | Specifier | Notes                           |
| ------------------- | --------- | ------------------------------- |
| `float`            | `%f`      | Promoted to double in printf    |
| `double`           | `%f`      | Standard double precision       |
| `long double`      | `%Lf`     | Extended precision (if supported) |

## **6. Complete Example**

```cpp
#include <iostream>
#include <cstdio>
#include <cmath>
using namespace std;

int main() {
    float PI = 3.14159265f;
    double precise_pi = 3.141592653589793;

    // Basic precision specification
    printf("Precision specification of %.*f \n", 1, PI);  // 3.1
    printf("Precision specification of %.*f\n", 2, PI);   // 3.14
    printf("Precision specification of %.*f\n", 3, PI);   // 3.142
    printf("Precision specification of %.*f\n", 4, PI);   // 3.1416

    // Width and alignment examples
    printf("Right aligned: '%10.3f'\n", PI);              // '     3.142'
    printf("Left aligned:  '%-10.3f'\n", PI);             // '3.142     '
    printf("Zero padded:   '%010.3f'\n", PI);             // '000003.142'

    // Different format specifiers
    printf("Fixed point:   %.6f\n", PI);                  // 3.141593
    printf("Scientific:    %.6e\n", PI);                  // 3.141593e+00
    printf("General:       %.6g\n", PI);                  // 3.14159
    printf("Uppercase sci: %.6E\n", PI);                  // 3.141593E+00

    // Lossless printing
    printf("Float lossless:  %.9g\n", PI);                // All significant digits
    printf("Double lossless: %.17g\n", precise_pi);       // All significant digits

    // Mathematical operations
    float x = 7.0f, y = 9.0f;
    printf("\nThe float division is: %.3f / %.3f = %.3f \n\n", 
           x, y, x / y);                                   // 7.000 / 9.000 = 0.778

    // Double precision
    double d = 12.45;
    printf("The double value is: %.3f \n", d);            // 12.450
    printf("The double value is: %.4f \n", d);            // 12.4500

    // Special values
    float infinity = 1.0f / 0.0f;
    float not_a_number = 0.0f / 0.0f;
    printf("Infinity: %f, %F\n", infinity, infinity);     // inf, INF
    printf("NaN: %f, %F\n", not_a_number, not_a_number); // nan, NAN

    // Combined width and precision with arguments
    int width = 12, precision = 4;
    printf("Dynamic format: %*.*f\n", width, precision, PI); // '      3.1416'

    return 0;
}
```

## **7. Key Points**

- **`%.*f`**: The `*` means the **precision will be taken from an argument**
- **Argument order**: For `%*.*f`, arguments are: width, precision, then the float value
- **Type promotion**: `float` arguments are automatically promoted to `double` in printf
- **Precision meaning**: For `%f`, precision specifies digits **after** the decimal point
- **Width vs Precision**: Width is total field size, precision is decimal places

## **8. Modern C++ Alternatives**

While `printf` remains widely used, modern C++ offers:

- **C++20 `std::format`**: Type-safe formatting with similar syntax
- **C++ streams**: `std::cout` with `std::fixed`, `std::setprecision()`, `std::setw()`
- **Third-party**: fmt library (basis for C++20's std::format)

```cpp
// Modern C++20 alternative
#include <format>
std::string result = std::format("{:.3f}", PI); // "3.142"
```

## **9. Best Practices**

1. Use `%g` format for general-purpose float printing to avoid trailing zeros
2. For lossless round-trip conversion, use appropriate precision: `.9g` for float, `.17g` for double
3. Always specify precision explicitly rather than relying on defaults
4. Use `%F` instead of `%f` when you want uppercase special value formatting