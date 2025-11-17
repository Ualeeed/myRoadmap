---
DONE: true
DATE: 2025-08-22T16:55:00
---

## What is Bitwise OR?

The **bitwise OR operator (`|`)** compares each bit of two numbers:

- If **at least one bit is 1** → result is 1
    
- If both are 0 → result is 0
    

It also works **bit by bit**.

## How It Works

The bitwise OR operator compares each bit at the same position in two numbers. The result bit is set to 1 if any of the corresponding bits is 1. Only when both bits are 0 does the result become 0. This operation is performed directly on the binary representation of numbers.

## Example

- Bitwise | (12 | 25): 

12 =<span style="color:rgb(255, 31, 31)"> 0000</span><span style="color:rgb(83, 233, 151)">11</span><span style="color:rgb(255, 31, 31)">00</span> (in Binary)
25 = <span style="color:rgb(255, 31, 31)">000</span><span style="color:rgb(83, 233, 151)">11</span><span style="color:rgb(255, 31, 31)">00</span><span style="color:rgb(83, 233, 151)">1</span> (in Binary)

<span style="color:rgb(255, 31, 31)">000</span><span style="color:rgb(83, 233, 151)">111</span><span style="color:rgb(255, 31, 31)">0</span><span style="color:rgb(83, 233, 151)">1</span> = 29 (in decimal)

```cpp
#include <iostream>
using namespace std;

int main()
{
	cout << "Result : " << (12 | 25);
	
	return 0;
}
```

## Common Use Cases

**Setting Specific Bits:**
- Used to turn on (set to 1) specific bits in a number
- Combines multiple bit flags together

**Combining Flags and Options:**
- Frequently used in hardware programming to set multiple flags
- Protocol design where different bits represent different features
- Managing permissions or settings where each bit represents a different option

**Low-Level Programming:**
- Device drivers for controlling hardware features
- Graphics programming for combining color channels
- Network protocol implementations
- Embedded systems programming

**Data Manipulation:**
- Merging data from different sources at bit level
- Creating bit masks by combining multiple values
- Building configuration settings from individual options

## Key Points

- The bitwise OR operator sets bits to 1 when at least one operand has that bit set
- Commonly used for enabling multiple flags or features simultaneously
- Essential in systems programming and hardware control
- Different from logical OR (`||`) which works with boolean values and uses short-circuit evaluation
- Works directly on integer types at the bit level