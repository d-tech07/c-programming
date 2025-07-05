
---

### **Unit 6: Functions in C (6 hrs)**

### **1. Introduction to Functions**

#### **Theory**
A **function** is a self-contained, reusable block of code that performs a specific task. Think of a large, complex program like building a car. You don't build the whole car in one go; you have separate teams for building the engine, the chassis, the transmission, etc. In C, functions are like those specialized teams.

The `main()` block in every C program is itself a function—it's just a special one that serves as the entry point for execution.

**Why use functions?**
*   **Modularity:** They break down a large, complex problem into smaller, manageable, and understandable pieces.
*   **Reusability (DRY Principle - Don't Repeat Yourself):** If you need to perform the same task multiple times, you can write a function once and call it whenever needed, instead of duplicating the code.
*   **Readability and Maintenance:** A program made of well-named functions is much easier to read and debug. `calculate_interest()` is more descriptive than a block of raw mathematical formulas.

**A function has three parts:**
1.  **Function Declaration (Prototype):** Informs the compiler about the function's name, return type, and parameters.
2.  **Function Call:** The statement that executes the function.
3.  **Function Definition:** The actual body of the function, containing the code that performs the task.

#### **Code Example (A Simple Function)**
This program defines and calls a simple function that prints a greeting.
```c
#include <stdio.h>

// --- Function Definition ---
// This function takes no input and returns nothing (void).
void printGreeting() {
    printf("*************************\n");
    printf("*   Welcome to my App   *\n");
    printf("*************************\n");
}

// --- Main Function (Entry Point) ---
int main() {
    printf("Program has started.\n");

    // --- Function Call ---
    // We are calling the printGreeting function to execute its code.
    printGreeting();

    printf("Program has ended.\n");
    return 0;
}
```

**Output:**
```
Program has started.
*************************
*   Welcome to my App   *
*************************
Program has ended.
```

---

### **2. Returning a Value from a Function**

#### **Theory**
A function can perform a calculation and send a result back to the code that called it. This is called **returning a value**.
*   The `return` keyword is used to send a value back.
*   The data type of the value the function returns must be specified before the function name in its definition (e.g., `int`, `double`).
*   A function that does not return any value has a return type of `void`.
*   When a `return` statement is executed, the function immediately terminates, and control is passed back to the caller.

#### **Code Example (Function that returns a sum)**
```c
#include <stdio.h>

// This function is defined to return an integer value.
int getSum() {
    int num1 = 10, num2 = 20;
    int sum = num1 + num2;
    return sum; // Send the value of 'sum' back to the caller.
}

int main() {
    int result;

    // Call getSum() and store the returned value in the 'result' variable.
    result = getSum();

    printf("The value returned from getSum() is: %d\n", result);
    return 0;
}
```

**Output:**
```
The value returned from getSum() is: 30
```

---

### **3. Sending a Value to a Function (Arguments)**

#### **Theory**
Often, a function needs input data to perform its task. We can pass values to a function when we call it.
*   **Parameters:** The variables listed in the function's definition that receive the input values (e.g., `int num1, int num2`).
*   **Arguments:** The actual values that are passed to the function during the function call (e.g., `5`, `x`).

**Pass-by-Value:**
In C, arguments are passed **by value** by default. This means the function receives a **copy** of the argument's value, not the original variable itself. Any changes made to the parameter inside the function **do not affect** the original argument in the calling code.

#### **Code Example (Function to calculate area)**
```c
#include <stdio.h>

// This function accepts two double values as parameters.
double calculateRectangleArea(double length, double width) {
    // 'length' and 'width' are local copies of the arguments passed.
    double area = length * width;
    return area;
}

int main() {
    double rectLength = 10.5;
    double rectWidth = 4.0;
    double area;

    // Pass 'rectLength' and 'rectWidth' as arguments to the function.
    area = calculateRectangleArea(rectLength, rectWidth);

    printf("The area of a rectangle with length %.2f and width %.2f is %.2f\n",
           rectLength, rectWidth, area);
    return 0;
}
```

**Output:**
```
The area of a rectangle with length 10.50 and width 4.00 is 42.00
```

---

### **4. Passing Arrays and Structures**

#### **Theory (Passing Arrays)**
When you pass an array to a function, you are not passing a copy of the entire array. Instead, you are passing the **memory address of the array's first element**. This is a form of **pass-by-reference**.

**Consequence:** Any modifications made to the array *inside* the function **will affect** the original array in the calling function. This is very different from passing simple variables like `int` or `double`. You also need to pass the size of the array as a separate argument because the function doesn't know how large the array is on its own.

#### **Code Example (Passing an Array)**
```c
#include <stdio.h>

// The function receives a pointer to the array's first element and its size.
void multiplyArrayByTwo(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        // This modification will change the original array in main().
        arr[i] = arr[i] * 2;
    }
}

int main() {
    int numbers[5] = {1, 2, 3, 4, 5};
    int size = 5;

    printf("Original array: ");
    for (int i = 0; i < size; i++) {
        printf("%d ", numbers[i]);
    }
    printf("\n");

    // Pass the array and its size to the function.
    multiplyArrayByTwo(numbers, size);

    printf("Array after function call: ");
    for (int i = 0; i < size; i++) {
        printf("%d ", numbers[i]);
    }
    printf("\n");

    return 0;
}
```

**Output:**
```
Original array: 1 2 3 4 5
Array after function call: 2 4 6 8 10
```

#### **Theory (Passing Structures)**
*   **By Value (Default):** Like simple variables, structs are passed by value by default. A full copy of the struct is created. This is safe but can be inefficient for large structs. You access members using the dot operator (`.`).
*   **By Reference (using Pointers - Preferred):** The more common and efficient method is to pass a pointer to the struct. This avoids copying the entire structure. You access members via a pointer using the arrow operator (`->`).

#### **Code Example (Passing a Structure)**
```c
#include <stdio.hh>

// Define a simple structure
struct Student {
    char name[50];
    int id;
};

// Function passing a struct by value (makes a copy)
void printStudentByValue(struct Student s) {
    printf("--- By Value ---\n");
    printf("Student Name: %s, ID: %d\n", s.name, s.id);
}

// Function passing a struct by reference (uses a pointer)
void printStudentByReference(struct Student *s_ptr) {
    printf("--- By Reference ---\n");
    // Use the arrow operator -> to access members via a pointer
    printf("Student Name: %s, ID: %d\n", s_ptr->name, s_ptr->id);
}

int main() {
    struct Student student1 = {"Alice", 101};

    // Call the functions
    printStudentByValue(student1);
    printStudentByReference(&student1); // Pass the address of the struct

    return 0;
}
```

**Output:**
```
--- By Value ---
Student Name: Alice, ID: 101
--- By Reference ---
Student Name: Alice, ID: 101
```

---

### **5. External Variables and Storage Classes**

#### **Theory**
A **storage class** in C determines a variable's scope (where it can be accessed), lifetime (how long it exists in memory), and initial value.

1.  **`auto` (Automatic):**
    *   **Scope:** Local to the block/function where it is declared.
    *   **Lifetime:** Created when the block is entered, destroyed when it is exited.
    *   **Default:** This is the default storage class for all local variables. The keyword `auto` is rarely used explicitly.

2.  **`extern` (External):**
    *   Used for **global variables** (declared outside any function).
    *   **Scope:** Global; visible to all functions in the program.
    *   **Lifetime:** Exists for the entire duration of the program.
    *   The `extern` keyword is used to *declare* a global variable that is *defined* in another source file, allowing you to share variables across multiple files.

3.  **`static`:**
    *   **Use 1 (Inside a function):** A static local variable's lifetime is the entire program run. It **retains its value between function calls**. Its scope is still local to the function.
    *   **Use 2 (Outside a function):** A static global variable's scope is restricted to the file in which it is declared. It cannot be accessed from other files, even with `extern`.

4.  **`register`:**
    *   A hint to the compiler to store the variable in a fast CPU register instead of RAM.
    *   Modern compilers are very good at optimization, so this keyword is rarely needed and often ignored.

#### **Code Example (Demonstrating `static` and `extern`)**
```c
#include <stdio.h>

// --- extern (Global) Variable ---
// This variable is defined here and is visible to all functions.
int global_count = 0;

void counterFunction() {
    // --- auto variable ---
    // 'local_count' is re-created and initialized to 1 every time.
    int local_count = 1;

    // --- static variable ---
    // 'static_count' is initialized to 1 only once.
    // It retains its value between calls.
    static int static_count = 1;

    printf("Local: %d, Static: %d, Global: %d\n",
           local_count, static_count, global_count);

    local_count++;
    static_count++;
    global_count++;
}

int main() {
    printf("Calling counterFunction multiple times:\n");
    counterFunction();
    counterFunction();
    counterFunction();
    return 0;
}
```

**Output:**
```
Calling counterFunction multiple times:
Local: 1, Static: 1, Global: 0
Local: 1, Static: 2, Global: 1
Local: 1, Static: 3, Global: 2
```

---

### **6. Preprocessor Directives, Libraries, Macros, Headers, and Prototyping**

#### **Theory**
These concepts govern how your source code is prepared before compilation and how multiple files are linked together.

*   **Preprocessor:** A program that processes your source code *before* it is passed to the compiler. It handles all directives that start with a hash (`#`).
*   **`#include`:** A preprocessor directive that includes the contents of another file.
    *   `#include <stdio.h>`: Includes a standard system library header file.
    *   `#include "my_header.h"`: Includes a user-defined header file from the current directory.
*   **C Libraries:** Collections of pre-compiled code (functions, types) that provide standard functionality (e.g., `stdio.h` for input/output, `string.h` for string manipulation).
*   **Macros (`#define`):** A preprocessor directive for creating constants or function-like macros. The preprocessor performs a direct text replacement.
    *   **Object-like Macro:** ` #define PI 3.14159`
    *   **Function-like Macro:** `#define SQUARE(x) ((x) * (x))`
        *   **Warning:** Always wrap macro arguments in parentheses `()` to avoid unexpected behavior due to operator precedence.
*   **Header Files (`.h`):** Files that contain function declarations (prototypes), macro definitions, and structure definitions. They are included in source files (`.c`) to share these declarations.
*   **Function Prototyping (Declaration):** A declaration that tells the compiler a function's name, return type, and the types of its parameters *before* the function is used. This allows you to call a function that is defined later in the file or in a different file.

#### **Code Example (A Multi-File Project)**

Let's create a project with three files: `main.c`, `utils.h`, and `utils.c`.

**File 1: `utils.h` (The Header File)**
This file contains the function prototype and a macro.
```c
// utils.h

// This is an "include guard" to prevent the header from being included multiple times.
#ifndef UTILS_H
#define UTILS_H

// --- Function Prototype ---
// Declares that a function named 'add' exists, which takes two ints and returns an int.
int add(int a, int b);

// --- Macro Definition ---
#define PI 3.14159

#endif // UTILS_H
```

**File 2: `utils.c` (The Implementation File)**
This file contains the actual definition of the `add` function.
```c
// utils.c

// Include its own header file to ensure consistency.
#include "utils.h"

// --- Function Definition ---
int add(int a, int b) {
    return a + b;
}
```

**File 3: `main.c` (The Main Program)**
This file uses the function and macro defined in the other files.
```c
// main.c

#include <stdio.h>
// Include our custom header file to get access to the 'add' prototype and 'PI' macro.
#include "utils.h"

int main() {
    int x = 10, y = 5;

    // Call the 'add' function, which is defined in utils.c
    int sum = add(x, y);

    printf("The sum of %d and %d is: %d\n", x, y, sum);

    // Use the 'PI' macro, which is defined in utils.h
    printf("The value of PI is: %f\n", PI);

    return 0;
}
```

**How to Compile (in a terminal):**
You must compile both `.c` files together.
```bash
gcc main.c utils.c -o my_program
```

**Output (when you run `./my_program`):**
```
The sum of 10 and 5 is: 15
The value of PI is: 3.141590
```