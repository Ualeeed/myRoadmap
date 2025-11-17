---
DONE: true
DATE: 2025-08-22T16:52:00
---

## What is Bitwise AND?

The **bitwise AND operator (`&`)** compares each bit of two numbers:

- If **both bits are 1** → result is 1
    
- Otherwise → result is 0
    

It works **bit by bit**.

## How It Works

The bitwise AND operator compares each bit at the same position in two numbers. The result bit is set to 1 only when both corresponding bits are 1. This operation is performed at the bit level within the CPU's arithmetic-logic unit.

## Example

- Bitwise & (12 & 25): 

12 = <span style="color:rgb(255, 31, 31)">0000</span><span style="color:rgb(83, 233, 151)">1</span><span style="color:rgb(83, 233, 151)">1</span><span style="color:rgb(255, 31, 31)">00 </span>(in Binary)
25 = <span style="color:rgb(255, 31, 31)">000</span><span style="color:rgb(83, 233, 151)">11</span><span style="color:rgb(255, 31, 31)">00</span><span style="color:rgb(83, 233, 151)">1</span> (in Binary)
 
<span style="color:rgb(255, 31, 31)">0000</span><span style="color:rgb(83, 233, 151)">1</span><span style="color:rgb(255, 31, 31)">000</span> = 8 (in decimal)

```cpp
#include <iostream>
using namespace std;

int main()
{
	cout << "Result : " << (12 & 25);
	
	return 0;
}
```

## Common Use Cases

**Checking Even/Odd Numbers:**
- Any even number `& 1` results in 0
- Any odd number `& 1` results in 1

**Bit Masking:**
- Used to extract specific bits from a number
- Allows manipulation of specific bits without affecting others

**Low-Level Programming:**
- Device drivers and hardware programming
- Communication protocol packet assembly
- Graphics programming at the bit level
- Memory-constrained embedded systems

**Data Compression & Encryption:**
- Used in compression algorithms to pack data efficiently
- Part of encryption algorithms to protect data

## Key Points

- The bitwise AND operator directly manipulates individual bits
- Particularly useful in lower-level programming where memory efficiency is critical
- Essential for working with hardware interfaces and binary protocols
- Different from logical AND (`&&`) which works with boolean values