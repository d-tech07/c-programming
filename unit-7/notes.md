
---

### **Unit 7: Pointers in C (7 hrs)**

### **1. Definition of Pointers**

#### **Theory**
A **pointer** is one of the most powerful and unique features of C. Simply put, a **pointer is a variable that stores the memory address of another variable**.

Instead of storing a value (like 10, 'A', or 3.14), a pointer stores the location where a value can be found. Think of your computer's memory as a huge street of houses, where each house has a unique address. A regular variable is like the contents inside a house (e.g., the family living there), while a pointer is a piece of paper on which you've written the address of that house.

**Two Key Pointer Operators:**
1.  **The Address-Of Operator (`&`):** When placed before a variable name, this operator returns the memory address of that variable.
2.  **The Dereference/Indirection Operator (`*`):** When placed before a pointer variable, this operator "goes to" the address stored in the pointer and retrieves the value stored at that address.

**Declaration:**
To declare a pointer, you use the `*` symbol between the data type and the variable name. The data type indicates the type of variable the pointer is intended to point to.
`data_type *pointer_name;`
`int *p;` // p is a pointer that can store the address of an integer variable.

#### **Code Example (Basic Pointer Operations)**
```c
#include <stdio.h>

int main() {
    int num = 10;      // A regular integer variable.
    int *ptr;          // A pointer variable that can point to an integer.

    // --- Storing an Address ---
    // The & operator gets the address of 'num'.
    // We store this address in the pointer 'ptr'.
    ptr = &num;

    printf("--- Values and Addresses ---\n");
    printf("Value of num: %d\n", num);
    printf("Address of num (&num): %p\n", &num);
    printf("Value of ptr (the address it holds): %p\n", ptr);
    printf("Address of the pointer itself (&ptr): %p\n", &ptr);

    // --- Dereferencing a Pointer ---
    // The * operator gets the value AT THE ADDRESS stored in ptr.
    printf("\nValue at the address pointed to by ptr (*ptr): %d\n", *ptr);

    // --- Modifying a variable using its pointer ---
    printf("\nChanging the value through the pointer...\n");
    *ptr = 25; // This changes the value at the address ptr holds, which is the value of 'num'.
    printf("New value of num: %d\n", num);

    return 0;
}
```

**Output:**
```
--- Values and Addresses ---
Value of num: 10
Address of num (&num): 0x7ffc3a5b8c94
Value of ptr (the address it holds): 0x7ffc3a5b8c94
Address of the pointer itself (&ptr): 0x7ffc3a5b8c98

Value at the address pointed to by ptr (*ptr): 10

Changing the value through the pointer...
New value of num: 25
```
*(Note: The exact hexadecimal addresses (`%p`) will be different every time you run the program.)*

---

### **2. Pointers for Arrays**

#### **Theory**
The name of an array, when used in an expression, **decays** into a pointer to its first element.
This means that `arr` is equivalent to `&arr[0]`.

This is a fundamental concept in C and explains why pointers and arrays are so closely related. You can use pointer syntax to access array elements.

#### **Code Example (Accessing an Array with Pointers)**
```c
#include <stdio.h>

int main() {
    int arr[5] = {10, 20, 30, 40, 50};
    int *ptr;

    // The array name 'arr' acts as a pointer to the first element.
    ptr = arr; // This is the same as ptr = &arr[0];

    printf("Accessing array elements using pointer:\n");
    for (int i = 0; i < 5; i++) {
        // *(ptr + i) is equivalent to arr[i]
        printf("Element at index %d: Value = %d, Address = %p\n",
               i, *(ptr + i), (ptr + i));
    }

    return 0;
}
```

**Output:**
```
Accessing array elements using pointer:
Element at index 0: Value = 10, Address = 0x7ffc9f2b8a70
Element at index 1: Value = 20, Address = 0x7ffc9f2b8a74
Element at index 2: Value = 30, Address = 0x7ffc9f2b8a78
Element at index 3: Value = 40, Address = 0x7ffc9f2b8a7c
Element at index 4: Value = 50, Address = 0x7ffc9f2b8a80
```
*(Notice the addresses are 4 bytes apart because an `int` on this system takes 4 bytes.)*

---

### **3. Returning Multiple Values from Functions Using Pointers**

#### **Theory**
A C function can only `return` one value. What if you need to get multiple results from a function (e.g., calculate both the sum and product of two numbers)? Pointers provide the solution.

Instead of returning values, you can pass the **addresses** of variables from your `main` function into the worker function. The worker function can then use these addresses (via pointers) to directly modify the original variables in `main`. This technique is called **pass-by-reference**.

#### **Code Example (Calculating Sum and Product)**
```c
#include <stdio.h>

// This function takes two numbers and two pointers as input.
// It will store the results directly into the memory locations pointed to by sum_ptr and prod_ptr.
void calculateSumAndProduct(int a, int b, int *sum_ptr, int *prod_ptr) {
    // Dereference the pointers to store the results.
    *sum_ptr = a + b;
    *prod_ptr = a * b;
}

int main() {
    int num1 = 10, num2 = 5;
    int sum_result, prod_result; // We want the function to fill these variables.

    // Pass the addresses of our result variables to the function.
    calculateSumAndProduct(num1, num2, &sum_result, &prod_result);

    printf("The numbers are %d and %d.\n", num1, num2);
    printf("Sum calculated by the function: %d\n", sum_result);
    printf("Product calculated by the function: %d\n", prod_result);

    return 0;
}
```

**Output:**
```
The numbers are 10 and 5.
Sum calculated by the function: 15
Product calculated by the function: 50
```

---

### **4. Pointer Arithmetic**

#### **Theory**
Pointer arithmetic is different from regular arithmetic. When you add an integer `n` to a pointer `p`, the result is not `p + n` bytes. The result is a new address that is `p + n * sizeof(*p)` bytes away.

In other words, incrementing a pointer moves it to the **next element** of its type, not the next byte.
*   `int *p; p++;` moves the address forward by `sizeof(int)` bytes (usually 4).
*   `double *d; d++;` moves the address forward by `sizeof(double)` bytes (usually 8).

This is why pointer arithmetic is so useful for navigating arrays.

#### **Code Example**
```c
#include <stdio.h>

int main() {
    int arr[] = {100, 200, 300};
    int *ptr = arr; // ptr points to 100

    printf("Initial pointer value: %p, points to value: %d\n", ptr, *ptr);

    // Incrementing the pointer
    ptr++; // Now ptr points to the next integer in memory (200)
    printf("After ptr++, pointer value: %p, points to value: %d\n", ptr, *ptr);

    // Decrementing the pointer
    ptr--; // Now ptr points back to the first integer (100)
    printf("After ptr--, pointer value: %p, points to value: %d\n", ptr, *ptr);

    return 0;
}
```

**Output:**
```
Initial pointer value: 0x7ffee3c67c2c, points to value: 100
After ptr++, pointer value: 0x7ffee3c67c30, points to value: 200
After ptr--, pointer value: 0x7ffee3c67c2c, points to value: 100
```

---

### **5. Pointers for Strings**

#### **Theory**
Since a string is just a `char` array ending in `\0`, a `char*` pointer is a very common way to work with strings. The pointer can be used to point to the beginning of the string, and pointer arithmetic can be used to traverse it.

#### **Code Example (Printing a string with a pointer)**
```c
#include <stdio.h>

void printString(const char *str_ptr) {
    // Loop until the pointer points to the null terminator '\0'.
    // The value of '\0' is 0, which is 'false' in a condition.
    while (*str_ptr) { // while (*str_ptr != '\0')
        printf("%c", *str_ptr);
        str_ptr++; // Move the pointer to the next character
    }
    printf("\n");
}

int main() {
    char message[] = "Pointers are fun!";
    printString(message);
    return 0;
}
```

**Output:**
```
Pointers are fun!
```

---

### **6. Double Indirection (Pointer to a Pointer)**

#### **Theory**
A **pointer to a pointer** is a variable that stores the memory address of another pointer. It is also called **double indirection**.

*   `int x;` // An integer
*   `int *p1;` // A pointer to an integer
*   `int **p2;` // A pointer to a pointer to an integer

`p2` holds the address of `p1`. `p1` holds the address of `x`.
To get the value of `x` from `p2`, you must dereference twice: `**p2`.

This is useful for functions that need to modify the pointer itself (not just the value it points to) and for creating dynamic 2D arrays (arrays of pointers).

#### **Code Example**
```c
#include <stdio.h>

int main() {
    int var = 789;
    int *ptr1;      // Pointer to int
    int **ptr2;     // Pointer to a pointer to int

    ptr1 = &var;    // ptr1 holds the address of var
    ptr2 = &ptr1;   // ptr2 holds the address of ptr1

    printf("Value of var = %d\n", var);

    // Accessing var's value using single pointer
    printf("Value of var using *ptr1 = %d\n", *ptr1);

    // Accessing var's value using double pointer
    printf("Value of var using **ptr2 = %d\n", **ptr2);

    printf("\n--- Addresses ---\n");
    printf("Address of var: %p\n", &var);
    printf("Address stored in ptr1: %p\n", ptr1);
    printf("Address of ptr1: %p\n", &ptr1);
    printf("Address stored in ptr2: %p\n", ptr2);

    return 0;
}
```

**Output:**
```
Value of var = 789
Value of var using *ptr1 = 789
Value of var using **ptr2 = 789

--- Addresses ---
Address of var: 0x7ffda3b1e93c
Address stored in ptr1: 0x7ffda3b1e93c
Address of ptr1: 0x7ffda3b1e940
Address stored in ptr2: 0x7ffda3b1e940
```

---

### **7. Pointer to Arrays**

#### **Theory**
This is a subtle but important concept. There is a difference between an **array of pointers** and a **pointer to an array**.

*   **Array of Pointers:** `int *arr[5];` This declares an array that holds 5 *pointers* to integers.
*   **Pointer to an Array:** `int (*ptr)[5];` This declares a single *pointer* that can point to an entire array of 5 integers. The parentheses around `*ptr` are crucial due to operator precedence.

When you increment a pointer to an array, it moves forward by the size of the *entire array*.

#### **Code Example**
```c
#include <stdio.h>

int main() {
    int arr[5] = {1, 2, 3, 4, 5};

    // 'ptr' is a pointer that can point to an array of 5 integers.
    int (*ptr)[5];
    ptr = &arr; // Assign the address of the whole array to the pointer.

    printf("Address of the whole array: %p\n", ptr);
    printf("Address after incrementing ptr: %p\n", ptr + 1);
    printf("Size of the array (sizeof(arr)): %zu bytes\n", sizeof(arr));

    // To access elements, you must first dereference the pointer to get the array,
    // then use the subscript.
    printf("\nAccessing elements:\n");
    for (int i = 0; i < 5; i++) {
        printf("Element %d: %d\n", i, (*ptr)[i]);
    }
    return 0;
}
```

**Output:**
```
Address of the whole array: 0x7ffdc1a6d9b0
Address after incrementing ptr: 0x7ffdc1a6d9c4
Size of the array (sizeof(arr)): 20 bytes

Accessing elements:
Element 0: 1
Element 1: 2
Element 2: 3
Element 3: 4
Element 4: 5
```
*(Notice the addresses are 20 bytes apart: `0x...c4` - `0x...b0` = 20. The pointer moved by the size of the whole array.)*

---

### **8. Dynamic Memory Allocation (`malloc` and `calloc`)**

#### **Theory**
So far, all our arrays had a fixed size determined at compile time. **Dynamic Memory Allocation** allows us to request memory from the operating system at **runtime**. This is essential when you don't know the amount of memory you need beforehand.

The functions for this are in the `<stdlib.h>` header.

**`malloc()` (memory allocation):**
*   Allocates a single, large block of memory of a specified size in bytes.
*   `void* malloc(size_t size);`
*   It returns a `void*` pointer (a generic pointer) to the beginning of the block. You must **cast** this pointer to the appropriate type (e.g., `(int*)`).
*   The memory it allocates is **not initialized**; it contains garbage values.
*   If `malloc` fails (e.g., the system is out of memory), it returns `NULL`. You **must always check for `NULL`**.

**`calloc()` (contiguous allocation):**
*   Allocates memory for an array of elements.
*   `void* calloc(size_t num_elements, size_t element_size);`
*   It has one key advantage over `malloc`: it **initializes all allocated bytes to zero**.

**`free()`:**
*   Memory allocated by `malloc` or `calloc` is stored on the **heap**. This memory is not automatically reclaimed when the function ends.
*   You are responsible for releasing it back to the system using `free()`.
*   `void free(void *ptr);`
*   Failure to `free` allocated memory results in a **memory leak**, where your program holds onto memory it no longer needs, potentially crashing the system.

#### **Code Example (Creating a dynamic array)**
```c
#include <stdio.h>
#include <stdlib.h> // Required for malloc, calloc, free

int main() {
    int n;
    int *arr;

    printf("Enter the number of elements for the dynamic array: ");
    scanf("%d", &n);

    // --- Allocate memory using malloc ---
    // We need space for 'n' integers. The size is n * sizeof(int).
    arr = (int*) malloc(n * sizeof(int));

    // --- ALWAYS check if malloc was successful ---
    if (arr == NULL) {
        printf("Error! Memory not allocated.\n");
        return 1; // Exit with an error code
    }

    printf("Memory successfully allocated using malloc.\n");

    // Store values in the dynamically allocated array
    for (int i = 0; i < n; i++) {
        arr[i] = i + 1;
    }

    // Print the elements
    printf("The elements of the array are: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");

    // --- CRITICAL STEP: Free the allocated memory ---
    free(arr);
    printf("Memory has been freed.\n");

    return 0;
}
```

**Output (Sample Run):**
```
Enter the number of elements for the dynamic array: 5
Memory successfully allocated using malloc.
The elements of the array are: 1 2 3 4 5
Memory has been freed.
```