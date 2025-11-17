---
DONE: true
DATE: 2025-08-22T23:28:00
---

# Two Dimensional Arrays in C++

## **1. What is a 2D Array?**

- A **two-dimensional (2D) array** is basically an **array of arrays**.
- The data inside the two-dimensional array in C++ can be visualized as a table (row-column manner). The location of each place in the two-dimensional arrays can be accessed using two variables, `i` and `j`, where `i` represents the row index and `j` represents the column index.
- It can be visualized as a table or a grid.

### Visual Representation

A 3×4 array looks like this:

```
Row/Col |  0   1   2   3
--------------------------
   0    |  10  20  30  40
   1    |  50  60  70  80
   2    |  90 100 110 120
```

**Memory Layout:** In memory, this 2D array is stored row by row (row-major order).

## **2. Declaration and Initialization**

### Basic Declaration
```c++
// Syntax: datatype arrayName[rows][columns];
int matrix[3][4];  // 3 rows, 4 columns
```

### Initialization Methods

**Method 1: During Declaration with Values**
```c++
int x[3][4] = { {1,2,3,4}, {5,6,7,8}, {9,10,11,12} };
```

**Method 2: Nested Initialization**
In a multi-dimensional array, each element in an array literal is another array literal.
```c++
string letters[2][4] = { 
    { "A", "B", "C", "D" }, 
    { "E", "F", "G", "H" } 
};
```

**Method 3: Partial Initialization**
```c++
int arr[3][3] = {{1,2}, {3,4,5}, {6}}; // Remaining elements are 0
```

## **3. Basic Example - Displaying a 2D Array**

```cpp
#include <iostream>
using namespace std;

int main()
{
    // Initialize a 3x4 2D array
    int x[3][4] = { {1,2,3,4}, {5,6,7,8}, {9,10,11,12} };

    // Display the array using nested loops
    for (int i = 0; i < 3; i++)
    {
        for (int j = 0; j < 4; j++)
        {
            cout << x[i][j] << " ";
        }
        cout << endl;
    }
    return 0;
}
```

**Output:**
```
		1 2 3 4 
		5 6 7 8 
		9 10 11 12 
```

## **4. Advanced Example - Multiplication Table**

```cpp
#include <cstdio>
#include <iostream>
using namespace std;

int main()
{
    int x[10][10];

    // Fill array with multiplication table
    for (int i = 0; i < 10; i++)
    {
        for (int j = 0; j < 10; j++)
        {
            x[i][j] = (i + 1) * (j + 1);
        }
    }

    // Display with formatted output
    for (int i = 0; i < 10; i++)
    {
        for (int j = 0; j < 10; j++)
        {
            printf("%0*d ", 2, x[i][j]);
        }
        cout << endl;
    }
    return 0;
}
```

## **5. Dynamic 2D Arrays**

It is just like a normal 2D or multi-dimensional array but it is implemented using pointers and memory allocation functions such as new and delete. The main point is that the size of this array is not fixed at compile time.

### Method 1: Array of Pointers
```cpp
#include <iostream>
using namespace std;

int main() {
    int rows = 3, cols = 4;
    
    // Create array of pointers
    int** arr = new int*[rows];
    
    // Allocate memory for each row
    for(int i = 0; i < rows; i++) {
        arr[i] = new int[cols];
    }
    
    // Initialize values
    int value = 1;
    for(int i = 0; i < rows; i++) {
        for(int j = 0; j < cols; j++) {
            arr[i][j] = value++;
        }
    }
    
    // Display array
    for(int i = 0; i < rows; i++) {
        for(int j = 0; j < cols; j++) {
            cout << arr[i][j] << " ";
        }
        cout << endl;
    }
    
    // Don't forget to deallocate memory
    for(int i = 0; i < rows; i++) {
        delete[] arr[i];
    }
    delete[] arr;
    
    return 0;
}
```

### Method 2: Single Block Allocation
```cpp
#include <iostream>
using namespace std;

int main() {
    int rows = 3, cols = 4;
    
    // Allocate single block of memory
    int* arr = new int[rows * cols];
    
    // Access using formula: arr[i*cols + j]
    int value = 1;
    for(int i = 0; i < rows; i++) {
        for(int j = 0; j < cols; j++) {
            arr[i * cols + j] = value++;
        }
    }
    
    // Display
    for(int i = 0; i < rows; i++) {
        for(int j = 0; j < cols; j++) {
            cout << arr[i * cols + j] << " ";
        }
        cout << endl;
    }
    
    delete[] arr;
    return 0;
}
```

## **6. Common Operations**

### Finding Maximum Element
```cpp
int findMax(int arr[][4], int rows, int cols) {
    int max = arr[0][0];
    for(int i = 0; i < rows; i++) {
        for(int j = 0; j < cols; j++) {
            if(arr[i][j] > max) {
                max = arr[i][j];
            }
        }
    }
    return max;
}
```

### Matrix Addition
```cpp
void addMatrices(int a[][3], int b[][3], int result[][3], int rows, int cols) {
    for(int i = 0; i < rows; i++) {
        for(int j = 0; j < cols; j++) {
            result[i][j] = a[i][j] + b[i][j];
        }
    }
}
```

### Transpose of Matrix
```cpp
void transpose(int matrix[][3], int transposed[][3], int rows, int cols) {
    for(int i = 0; i < rows; i++) {
        for(int j = 0; j < cols; j++) {
            transposed[j][i] = matrix[i][j];
        }
    }
}
```

## **7. Modern C++ Approaches**

### Using std::array for Fixed Size
When initializing a multidimensional std::array, we need to use double-braces
```cpp
#include <array>
#include <iostream>
using namespace std;

int main() {
    std::array<std::array<int, 4>, 3> arr {{
        { 1, 2, 3, 4 },
        { 5, 6, 7, 8 },
        { 9, 10, 11, 12 }
    }};
    
    // Access elements
    for(const auto& row : arr) {
        for(int val : row) {
            cout << val << " ";
        }
        cout << endl;
    }
    
    return 0;
}
```

### Using std::vector for Dynamic Size
```cpp
#include <vector>
#include <iostream>
using namespace std;

int main() {
    int rows = 3, cols = 4;
    
    // Create 2D vector
    vector<vector<int>> matrix(rows, vector<int>(cols));
    
    // Initialize
    int value = 1;
    for(int i = 0; i < rows; i++) {
        for(int j = 0; j < cols; j++) {
            matrix[i][j] = value++;
        }
    }
    
    // Display using range-based for loop
    for(const auto& row : matrix) {
        for(int val : row) {
            cout << val << " ";
        }
        cout << endl;
    }
    
    return 0;
}
```

## **8. Important Points to Remember**

1. **Column size must be specified** when passing 2D arrays to functions
2. **Memory is allocated row by row** (row-major order)
3. **Always deallocate dynamically allocated memory** to prevent memory leaks
4. **Index starts from 0** for both rows and columns
5. **Bounds checking** is not automatic - accessing out-of-bounds causes undefined behavior

## **9. Common Pitfalls**

1. **Forgetting to deallocate memory** in dynamic arrays
2. **Array decay** when passing to functions
3. **Incorrect indexing** leading to segmentation faults
4. **Mixed up row/column indices**


*This comprehensive guide covers both basic and advanced concepts of 2D arrays in C++, providing a solid foundation for working with multidimensional data structures.
