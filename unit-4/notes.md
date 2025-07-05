

### **Unit 4: Control Structures in C**

### **1. Introduction to Control Structures**

#### **Theory**
By default, a C program executes its code **sequentially**, meaning it runs statements one after another from top to bottom. This is like following a recipe step-by-step without any options. However, to create powerful and intelligent programs, we need to alter this rigid flow.

**Control Structures** are statements that allow a programmer to control the order in which instructions are executed. They are the decision-making and repetition mechanisms of the language, enabling the program to choose different paths or repeat actions based on given conditions.

There are three main categories of control flow:
1.  **Sequential:** The default top-to-bottom execution.
2.  **Branching (or Selection):** Choosing a path among alternatives (`if`, `switch`).
3.  **Looping (or Iteration):** Repeating a block of code (`while`, `do-while`, `for`).

---

### **2. Branching Statements**

Branching statements allow a program to execute specific blocks of code while skipping others, based on whether a condition is true or false.

#### **A. The `if` Statement**

**Theory:**
The `if` statement is the most basic decision-making statement. It evaluates a condition (a relational or logical expression). If the condition is `true` (evaluates to a non-zero value), the block of code inside the `if` statement is executed. If the condition is `false` (evaluates to 0), the block is skipped entirely.

**Code Example:**
This program checks if a user is old enough to get a driver's license.
```c
#include <stdio.h>

int main() {
    int age;
    printf("Please enter your age: ");
    scanf("%d", &age);

    // The condition is (age >= 16)
    if (age >= 16) {
        printf("You are old enough to apply for a driver's license.\n");
    }

    printf("This line always runs, regardless of age.\n");
    return 0;
}
```

**Output (Sample Run 1: Condition is True)**
```
Please enter your age: 19
You are old enough to apply for a driver's license.
This line always runs, regardless of age.
```

**Output (Sample Run 2: Condition is False)**
```
Please enter your age: 14
This line always runs, regardless of age.
```

#### **B. The `if-else` Statement**

**Theory:**
The `if-else` statement provides an alternative path for when the `if` condition is false. If the condition is `true`, the `if` block is executed. If the condition is `false`, the `else` block is executed. One of the two blocks will *always* be executed.

**Code Example:**
This program determines if a number entered by the user is even or odd.
```c
#include <stdio.h>

int main() {
    int number;
    printf("Enter an integer: ");
    scanf("%d", &number);

    // If the number is perfectly divisible by 2, it's even.
    if (number % 2 == 0) {
        printf("The number %d is EVEN.\n", number);
    } else {
        // Otherwise, it must be odd.
        printf("The number %d is ODD.\n", number);
    }
    return 0;
}
```

**Output (Sample Run 1: `if` block executes)**
```
Enter an integer: 42
The number 42 is EVEN.
```

**Output (Sample Run 2: `else` block executes)**
```
Enter an integer: 77
The number 77 is ODD.
```

#### **C. The `if-else-if` Ladder**

**Theory:**
This structure, often called an "else-if ladder," is used to test a series of conditions. The conditions are evaluated from top to bottom. As soon as a `true` condition is found, its corresponding block is executed, and the rest of the ladder is skipped. The final `else` block is a default case that runs only if *none* of the preceding conditions are true.

**Code Example:**
This program checks if a number is positive, negative, or zero.
```c
#include <stdio.h>

int main() {
    int number;
    printf("Enter any integer: ");
    scanf("%d", &number);

    if (number > 0) {
        printf("The number is POSITIVE.\n");
    } else if (number < 0) {
        printf("The number is NEGATIVE.\n");
    } else {
        printf("The number is ZERO.\n");
    }
    return 0;
}
```

**Output (Sample Run 1)**
```
Enter any integer: 25
The number is POSITIVE.
```

**Output (Sample Run 2)**
```
Enter any integer: -10
The number is NEGATIVE.
```

**Output (Sample Run 3)**
```
Enter any integer: 0
The number is ZERO.
```

#### **D. The `switch` Statement**

**Theory:**
The `switch` statement is an efficient alternative to a long `if-else-if` ladder when the condition involves comparing a single variable against multiple constant integer or character values.

*   `switch(expression)`: The `expression` is evaluated once.
*   `case value:`: The result of the expression is compared with each `case` value.
*   `break;`: When a matching `case` is found, the code block is executed until a `break` statement is encountered. The `break` causes an immediate exit from the `switch` block. **If you forget `break`, execution "falls through" to the next case, which is a common bug.**
*   `default:`: If no `case` values match the expression, the `default` block is executed. It is optional.

**Code Example:**
This program acts as a simple vending machine menu.
```c
#include <stdio.hh>

int main() {
    int choice;
    printf("--- Vending Machine ---\n");
    printf("1. Cola\n");
    printf("2. Crisps\n");
    printf("3. Chocolate\n");
    printf("4. Water\n");
    printf("Enter your choice (1-4): ");
    scanf("%d", &choice);

    switch (choice) {
        case 1:
            printf("Dispensing Cola. Price: $1.50\n");
            break;
        case 2:
            printf("Dispensing Crisps. Price: $1.00\n");
            break;
        case 3:
            printf("Dispensing Chocolate. Price: $1.25\n");
            break;
        case 4:
            printf("Dispensing Water. Price: $0.75\n");
            break;
        default:
            printf("Invalid choice. Please select from 1-4.\n");
            break;
    }
    printf("Thank you for using the vending machine!\n");
    return 0;
}
```

**Output (Sample Run 1)**
```
--- Vending Machine ---
1. Cola
2. Crisps
3. Chocolate
4. Water
Enter your choice (1-4): 3
Dispensing Chocolate. Price: $1.25
Thank you for using the vending machine!
```

**Output (Sample Run 2 - Default case)**
```
--- Vending Machine ---
1. Cola
2. Crisps
3. Chocolate
4. Water
Enter your choice (1-4): 7
Invalid choice. Please select from 1-4.
Thank you for using the vending machine!
```
---

### **3. Looping Statements**

Looping statements allow a block of code to be executed repeatedly as long as a condition is true.

#### **A. The `while` Loop**

**Theory:**
A `while` loop is an **entry-controlled loop**. This means the condition is checked *before* the loop body is executed. If the condition is false the first time it is checked, the loop body will not execute even once. It's essential that the body of the loop contains a statement that eventually makes the condition false, otherwise, you'll create an infinite loop.

**Code Example:**
This program prints the numbers from 5 down to 1.
```c
#include <stdio.h>

int main() {
    int count = 5; // 1. Initialization

    printf("Countdown starting...\n");

    while (count >= 1) { // 2. Condition
        printf("%d...\n", count);
        count--; // 3. Update (decrement the counter)
    }

    printf("Blast off!\n");
    return 0;
}
```

**Output:**
```
Countdown starting...
5...
4...
3...
2...
1...
Blast off!
```

#### **B. The `do-while` Loop**

**Theory:**
A `do-while` loop is an **exit-controlled loop**. This means the loop body is executed *first*, and *then* the condition is checked at the end. This guarantees that the loop body will be executed at least one time, regardless of whether the condition is true or false. This is very useful for things like input validation. Note the required semicolon `;` after the `while(condition)`.

**Code Example:**
This program repeatedly asks the user to guess a secret number until they guess correctly. The loop must run at least once for them to make their first guess.
```c
#include <stdio.h>

int main() {
    const int SECRET_NUMBER = 7;
    int guess;

    do {
        printf("Guess the secret number (1-10): ");
        scanf("%d", &guess);

        if (guess != SECRET_NUMBER) {
            printf("Wrong guess! Try again.\n");
        }
    } while (guess != SECRET_NUMBER); // Condition is checked at the end

    printf("Congratulations! You guessed the secret number: %d\n", SECRET_NUMBER);
    return 0;
}
```

**Output (Sample Run):**
```
Guess the secret number (1-10): 3
Wrong guess! Try again.
Guess the secret number (1-10): 8
Wrong guess! Try again.
Guess the secret number (1-10): 7
Congratulations! You guessed the secret number: 7
```

#### **C. The `for` Loop**

**Theory:**
The `for` loop is often the preferred choice when you know in advance how many times you want to repeat the loop. It is a very structured loop that combines the three essential loop components—initialization, condition, and update—into a single, easy-to-read line.
`for (initialization; condition; update)`
1.  **Initialization:** Executed only once, at the very beginning.
2.  **Condition:** Checked before each iteration. If false, the loop terminates.
3.  **Update:** Executed at the end of each iteration, after the loop body.

**Code Example:**
This program calculates the factorial of a number (e.g., 5! = 5 * 4 * 3 * 2 * 1).
```c
#include <stdio.h>

int main() {
    int number;
    long long factorial = 1; // Use long long for larger factorial values

    printf("Enter a non-negative integer: ");
    scanf("%d", &number);

    // for loop to calculate factorial
    // i starts at the number and decrements to 1
    for (int i = number; i >= 1; i--) {
        factorial = factorial * i;
    }

    printf("Factorial of %d = %lld\n", number, factorial);
    return 0;
}
```

**Output:**
```
Enter a non-negative integer: 5
Factorial of 5 = 120
```

#### **D. Nested Loops**

**Theory:**
A nested loop is simply a loop that exists inside the body of another loop. The inner loop executes all of its iterations for each single iteration of the outer loop. This is a common pattern for working with two-dimensional data, like grids, tables, or matrices, or for printing patterns.

**Code Example:**
This program uses a nested `for` loop to print a 4x5 rectangle of hash symbols (`#`).
```c
#include <stdio.h>

int main() {
    int rows = 4;
    int columns = 5;

    // Outer loop controls the rows
    for (int i = 1; i <= rows; i++) {
        // Inner loop controls the columns for the current row
        for (int j = 1; j <= columns; j++) {
            printf("# ");
        }
        // After the inner loop completes, print a newline to move to the next row
        printf("\n");
    }
    return 0;
}
```

**Output:**
```
# # # # #
# # # # #
# # # # #
# # # # #
```

---

### **4. Jump Statements**

Jump statements cause an unconditional transfer of control from one part of a program to another.

#### **A. `break` Statement**

**Theory:**
We already saw `break` in the `switch` statement. When used inside a `for`, `while`, or `do-while` loop, `break` causes the **immediate termination of the loop**. Program control is transferred to the first statement *after* the loop.

**Code Example:**
This program searches for the first negative number in a list. Once found, it stops searching.
```c
#include <stdio.h>

int main() {
    int values[] = {15, 22, 10, -5, 30, 8};
    int i;

    for (i = 0; i < 6; i++) {
        if (values[i] < 0) {
            printf("First negative number found: %d at index %d.\n", values[i], i);
            break; // Exit the loop immediately
        }
        printf("Checked value: %d\n", values[i]);
    }

    printf("Loop terminated.\n");
    return 0;
}
```

**Output:**
```
Checked value: 15
Checked value: 22
Checked value: 10
First negative number found: -5 at index 3.
Loop terminated.
```

#### **B. `continue` Statement**

**Theory:**
The `continue` statement is also used inside loops. Instead of terminating the loop, it forces the **immediate start of the next iteration**, skipping any code that comes after it within the loop body for the current iteration.

**Code Example:**
This program processes a list of transactions but skips any transaction with a value of 0.
```c
#include <stdio.h>

int main() {
    int transactions[] = {100, -50, 0, 200, -75, 0, 120};
    int i;

    for (i = 0; i < 7; i++) {
        if (transactions[i] == 0) {
            printf("Skipping zero-value transaction at index %d.\n", i);
            continue; // Skip the rest of this iteration
        }
        printf("Processing transaction of value: %d\n", transactions[i]);
    }

    printf("All transactions processed.\n");
    return 0;
}
```

**Output:**
```
Processing transaction of value: 100
Processing transaction of value: -50
Skipping zero-value transaction at index 2.
Processing transaction of value: 200
Processing transaction of value: -75
Skipping zero-value transaction at index 5.
Processing transaction of value: 120
All transactions processed.
```

#### **C. `goto` Statement**

**Theory:**
The `goto` statement provides a way to jump unconditionally to a designated label within the same function. A label is an identifier followed by a colon (e.g., `my_label:`).

**WARNING:** The use of `goto` is highly discouraged in modern C programming. It can make code flow confusing, hard to read, and difficult to debug, a situation often called "spaghetti code." It is almost always possible to solve a problem more cleanly using structured control flow (`if`, `while`, `for`, functions). It is included here for academic completeness.

**Code Example:**
A contrived example showing `goto` used for error handling.
```c
#include <stdio.h>

int main() {
    double num, result;
    printf("Enter a number to find its square root: ");
    scanf("%lf", &num);

    if (num < 0) {
        goto error_handler; // Jump to the error label
    }

    // This part is skipped if num is negative
    result = sqrt(num); // Assuming #include <math.h> for sqrt
    printf("The square root of %.2lf is %.2lf\n", num, result);
    goto end; // Jump over the error handler to the end

error_handler:
    printf("Error: Cannot calculate the square root of a negative number.\n");

end:
    printf("Program finished.\n");
    return 0;
}
```

**Output (Sample Run):**
```
Enter a number to find its square root: -9
Error: Cannot calculate the square root of a negative number.
Program finished.
```