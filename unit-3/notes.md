
### **Unit 3: Variables and Data Types in C**

### **Introduction: The Building Blocks of Data**

Every useful program needs to work with data. This data could be a user's age, the price of an item, a character in a name, or the result of a calculation. In programming, we need a way to store this data in the computer's memory so we can use it and manipulate it. This is where **variables** and **constants** come in.

Think of a variable as a labeled box where you can store information. The **label** is the variable's name, and the **contents** are its value. The **type** of the box determines what kind of information it can hold (e.g., a box for numbers, a box for letters).

---

### **1. Constants and Variables**

#### **A. Variables**

A **variable** is a named location in the computer's memory that stores a value. The key characteristic of a variable is that its value can be **changed** during the execution of the program.

**Theory:**
*   **Named Memory:** Instead of remembering a complex memory address like `0x7ffee1a38abc`, we give it a simple, human-readable name like `userAge`.
*   **Mutable:** The value stored at that location can be updated or overwritten.

**C Code Example:**
```c
#include <stdio.h>

int main() {
    // 'score' is a variable of type integer.
    // It is initialized with the value 100.
    int score = 100;
    printf("The initial score is: %d\n", score);

    // The value of the variable 'score' is changed.
    score = 150;
    printf("The updated score is: %d\n", score);

    // We can even change its value based on its previous value.
    score = score + 20;
    printf("The final score is: %d\n", score);

    return 0;
}
```
**Output:**
```
The initial score is: 100
The updated score is: 150
The final score is: 170
```

#### **B. Constants**

A **constant** is a value that, once defined, **cannot be changed** during the program's execution. Using constants makes your program more readable and safer by preventing accidental modification of critical values.

There are two primary ways to define constants in C:

**1. The `const` Keyword (Preferred Method)**
This creates a read-only variable. It's type-safe and respects scope (meaning it's only known within the block it's defined in).

**Theory:**
*   The `const` qualifier tells the compiler that the variable is read-only.
*   Any attempt to modify a `const` variable will result in a compile-time error.

**C Code Example:**
```c
#include <stdio.h>

int main() {
    // 'PI' is a constant of type double.
    const double PI = 3.14159;
    printf("The value of PI is: %lf\n", PI);

    // The following line, if uncommented, will cause a compiler error:
    // PI = 3.14; // ERROR: assignment of read-only variable 'PI'

    double radius = 5.0;
    double area = PI * radius * radius;
    printf("The area of a circle with radius 5.0 is: %lf\n", area);

    return 0;
}
```

**2. The `#define` Preprocessor Directive**
This is an older method. The preprocessor replaces every occurrence of the identifier with the value *before* the code is actually compiled. It's a simple text-replacement mechanism.

**Theory:**
*   `#define` is a preprocessor command, not part of the C language itself.
*   It does not allocate memory in the same way a variable does.
*   It is not type-safe (it's just text).

**C Code Example:**
```c
#include <stdio.h>

// The preprocessor will replace every instance of 'SECONDS_PER_MINUTE' with '60'
#define SECONDS_PER_MINUTE 60

int main() {
    int minutes = 10;
    int totalSeconds = minutes * SECONDS_PER_MINUTE;

    printf("%d minutes is equal to %d seconds.\n", minutes, totalSeconds);

    return 0;
}
```

---

### **2. Variable Declaration**

Before you can use a variable, you must **declare** it. A declaration tells the compiler the variable's **name** and its **data type**.

**Syntax:** `data_type variable_name;`

*   **`data_type`:** The type of data the variable will hold (e.g., `int`, `float`, `char`).
*   **`variable_name`:** The name you choose for the variable.

**Rules for Naming Variables (Identifiers) in C:**
1.  Can contain letters (`a-z`, `A-Z`), digits (`0-9`), and the underscore character (`_`).
2.  Must begin with a letter or an underscore. It cannot begin with a number.
3.  C is **case-sensitive**. `age` and `Age` are two different variables.
4.  You cannot use C **keywords** (like `int`, `if`, `return`) as variable names.

**Declaration vs. Initialization**
*   **Declaration:** Reserving the memory space (the box). `int height;`
*   **Initialization:** Giving the variable an initial value at the time of declaration. `int height = 180;`

**It is extremely good practice to always initialize your variables.** An uninitialized variable holds a "garbage value"—whatever random data was previously in that memory location.

**C Code Example:**
```c
#include <stdio.h>

int main() {
    // --- Variable Declarations ---
    int studentAge;        // Declared but not initialized (contains garbage value)
    double itemPrice;      // Declared but not initialized
    char grade;            // Declared but not initialized

    // --- Variable Initialization ---
    int numberOfStudents = 25; // Declared AND initialized
    double accountBalance = 1050.75;
    char middleInitial = 'M';

    // --- Using the variables ---
    // Let's assign values to the declared variables
    studentAge = 21;
    itemPrice = 19.99;
    grade = 'A';

    printf("Age: %d, Number of Students: %d\n", studentAge, numberOfStudents);
    printf("Price: %.2f, Balance: %.2f\n", itemPrice, accountBalance);
    printf("Grade: %c, Middle Initial: %c\n", grade, middleInitial);

    // Example of an uninitialized variable (its value is unpredictable)
    int uninitializedVar;
    printf("Value of uninitialized variable: %d\n", uninitializedVar); // This will print a random number!

    return 0;
}
```

---

### **3. Variable Types (Data Types)**

The **data type** defines the kind of value a variable can hold and the amount of memory it occupies. Choosing the correct data type is essential for writing efficient and correct programs.

#### **Primary (Basic) Data Types**

| Type | Description | Size (Typical) | Format Specifier | Example |
| :--- | :--- | :--- | :--- | :--- |
| `int` | Integer. For whole numbers (positive, negative, or zero). | 4 bytes | `%d` | `10`, `-5`, `0` |
| `float` | Floating-point. For decimal numbers (single precision). | 4 bytes | `%f` | `3.14`, `-0.05` |
| `double` | Double-precision floating-point. For decimal numbers with higher precision. | 8 bytes | `%lf` | `3.1415926535`|
| `char` | Character. For a single character, enclosed in single quotes. | 1 byte | `%c` | `'A'`, `'g'`, `'5'` |

**Note on `char`:** A `char` is internally stored as an integer (its ASCII value). For example, the character `'A'` is stored as the number 65.

#### **Type Modifiers**
Modifiers like `short`, `long`, `signed`, and `unsigned` can be used to alter the size or range of a basic data type.

*   `short int`: A smaller integer.
*   `long int`: A larger integer.
*   `long long int`: An even larger integer.
*   `unsigned int`: An integer that can only hold non-negative values (0 and positive), effectively doubling its maximum positive range.

**C Code Example (`sizeof` operator):**
The `sizeof` operator is a built-in C function that tells you how many bytes a data type occupies on your specific machine.

```c
#include <stdio.h>

int main() {
    printf("Size of int: %zu bytes\n", sizeof(int));
    printf("Size of short int: %zu bytes\n", sizeof(short int));
    printf("Size of long int: %zu bytes\n", sizeof(long int));
    printf("Size of float: %zu bytes\n", sizeof(float));
    printf("Size of double: %zu bytes\n", sizeof(double));
    printf("Size of char: %zu bytes\n", sizeof(char));

    return 0;
}
```
*(Note: `%zu` is the correct format specifier for the result of `sizeof`)*

---

### **4. Simple Input/Output Functions**

To make our programs interactive, we need to get data *from* the user (input) and display results *to* the user (output). In C, this is commonly done with `scanf` and `printf`.

#### **Output: `printf()` ("print formatted")**
`printf` displays text and variable values on the console. It uses **format specifiers** (like `%d`, `%f`) as placeholders for the variables you want to print.

#### **Input: `scanf()` ("scan formatted")**
`scanf` reads data from the keyboard and stores it in variables. It also uses format specifiers to know what kind of data to expect.

**CRITICAL:** When using `scanf`, you must pass the **memory address** of the variable where the data should be stored. You get the address of a variable by using the ampersand `&` (the "address-of" operator).

**C Code Example (A Complete I/O Program):**
This program asks the user for their initials, age, and GPA, then prints it back to them.

```c
#include <stdio.h>

int main() {
    // 1. Declare variables to store user data
    char firstInitial;
    char lastInitial;
    int age;
    double gpa;

    // 2. Get input from the user using printf (for prompts) and scanf (for reading)
    printf("Enter your first initial: ");
    scanf(" %c", &firstInitial); // The space before %c is important! It consumes whitespace.

    printf("Enter your last initial: ");
    scanf(" %c", &lastInitial);

    printf("Enter your age: ");
    scanf("%d", &age); // Use & to pass the memory address

    printf("Enter your GPA: ");
    scanf("%lf", &gpa); // Use %lf for reading a double

    // 3. Display the collected data using printf
    printf("\n--- User Profile ---\n");
    printf("Initials: %c.%c.\n", firstInitial, lastInitial);
    printf("Age: %d years old\n", age);
    printf("GPA: %.2lf\n", gpa); // %.2lf formats to 2 decimal places

    return 0;
}
```

---

### **5. Operators**

In C, an **operator** is a symbol that tells the compiler to perform a specific mathematical, relational, or logical operation. Think of them as the verbs of the C language—they perform actions on data. The data items that operators act upon are called **operands**.

For example, in the expression `a + b`, `+` is the operator, and `a` and `b` are the operands.


Operators are special symbols that perform operations on variables and values (operands).

#### **A. Arithmetic Operators**
Used for mathematical calculations.

| Operator | Name | Example | Result |
| :--- | :--- | :--- | :--- |
| `+` | Addition | `x + y` | Sum of x and y |
| `-` | Subtraction | `x - y` | Difference of x and y |
| `*` | Multiplication | `x * y` | Product of x and y |
| `/` | Division | `x / y` | Quotient of x and y |
| `%` | Modulus | `x % y` | Remainder of `x / y` (only works with integers) |

**C Code Example:**
```c
#include <stdio.h>

int main() {
    int a = 10;
    int b = 3;

    printf("a + b = %d\n", a + b); // 13
    printf("a - b = %d\n", a - b); // 7
    printf("a * b = %d\n", a * b); // 30
    printf("a / b = %d\n", a / b); // 3 (Integer division truncates the decimal)
    printf("a %% b = %d\n", a % b); // 1 (The remainder of 10 / 3)

    // To get proper decimal division, use floating-point types
    double x = 10.0;
    double y = 3.0;
    printf("x / y = %lf\n", x / y); // 3.333333

    return 0;
}
```

#### **B. Other Important Operator Types (Brief Overview)**

*   **Assignment Operators:** Used to assign values to variables.
    *   `=` (Simple assignment): `x = 10;`
    *   `+=`, `-=`, `*=`, `/=`, `%=` (Compound assignment): `x += 5;` is shorthand for `x = x + 5;`

*   **Relational Operators:** Used to compare two values. They result in either `1` (true) or `0` (false).
    *   `==` (Equal to)
    *   `!=` (Not equal to)
    *   `>` (Greater than)
    *   `<` (Less than)
    *   `>=` (Greater than or equal to)
    *   `<=` (Less than or equal to)

*   **Logical Operators:** Used to combine or invert boolean conditions.
    *   `&&` (Logical AND): `(x > 5) && (y < 10)` is true only if both conditions are true.
    *   `||` (Logical OR): `(x > 5) || (y < 10)` is true if at least one condition is true.
    *   `!` (Logical NOT): `!(x > 5)` is true if `x > 5` is false.

*   **Increment/Decrement Operators:**
    *   `++` (Increment): Increases the value of an integer by 1. `x++;`
    *   `--` (Decrement): Decreases the value of an integer by 1. `x--;`


    Of course. Here is a highly detailed guide to operators in C, covering their categories, behavior, precedence, and providing clear, commented code examples for each.

---

### **Introduction: What Are Operators?**


C operators can be broadly classified into the following categories:
1.  **Arithmetic Operators**
2.  **Relational Operators**
3.  **Logical Operators**
4.  **Assignment Operators**
5.  **Increment and Decrement Operators**
6.  **Bitwise Operators**
7.  **Miscellaneous Operators** (including `sizeof` and the ternary operator)

---

### **1. Arithmetic Operators**

These operators are used to perform mathematical calculations like addition, subtraction, multiplication, etc.

| Operator | Name | Description | Example |
| :--- | :--- | :--- | :--- |
| `+` | Addition | Adds two operands. | `x + y` |
| `-` | Subtraction | Subtracts the second operand from the first. | `x - y` |
| `*` | Multiplication | Multiplies two operands. | `x * y` |
| `/` | Division | Divides the first operand by the second. | `x / y` |
| `%` | Modulus | Returns the remainder of an integer division. | `x % y` |

#### **Key Concepts and Pitfalls:**

*   **Integer Division:** When you divide two integers, the result will also be an integer, and the fractional part is **truncated** (cut off). For example, `7 / 2` evaluates to `3`, not `3.5`.
*   **Floating-Point Division:** To get a precise decimal result, at least one of the operands must be a floating-point type (`float` or `double`). For example, `7.0 / 2` evaluates to `3.5`.
*   **Modulus Operator (`%`):** This operator only works with integer operands. It's incredibly useful for tasks like checking if a number is even or odd (`number % 2 == 0`).

#### **C Code Example:**

```c
#include <stdio.h>

int main() {
    int a = 10, b = 4;
    double x = 10.0, y = 4.0;

    printf("--- Arithmetic with Integers ---\n");
    printf("a + b = %d\n", a + b);       // 14
    printf("a - b = %d\n", a - b);       // 6
    printf("a * b = %d\n", a * b);       // 40
    printf("a / b = %d (Integer Division!)\n", a / b); // 2 (10/4 is 2.5, .5 is truncated)
    printf("a %% b = %d (Remainder)\n", a % b); // 2 (10 divided by 4 is 2 with a remainder of 2)

    printf("\n--- Arithmetic with Doubles ---\n");
    printf("x / y = %lf\n", x / y);       // 2.500000
    printf("x / a = %lf\n", x / a);       // 1.000000 (A double divided by an int results in a double)

    return 0;
}
```

---

### **2. Relational Operators**

These operators are used to compare two values. The result of a relational operation is a boolean value: either `1` (for true) or `0` (for false).

| Operator | Name | Example | Returns `1` (true) if... |
| :--- | :--- | :--- | :--- |
| `==` | Equal to | `x == y` | `x` is exactly equal to `y` |
| `!=` | Not equal to | `x != y` | `x` is not equal to `y` |
| `>` | Greater than | `x > y` | `x` is greater than `y` |
| `<` | Less than | `x < y` | `x` is less than `y` |
| `>=` | Greater than or equal to | `x >= y` | `x` is greater than or equal to `y` |
| `<=` | Less than or equal to | `x <= y` | `x` is less than or equal to `y` |

#### **CRITICAL PITFALL: `==` (Comparison) vs. `=` (Assignment)**

This is the most common bug for new C programmers.
*   `if (x == 5)` asks the question: "Is the value of x equal to 5?" (Correct for comparisons).
*   `if (x = 5)` performs an action: "Assign the value 5 to x, and the value of this entire expression is 5." Since C treats any non-zero value as `true`, this `if` statement will *always* be true, and it will silently change the value of `x`.

#### **C Code Example:**

```c
#include <stdio.h>

int main() {
    int a = 5, b = 10;

    printf("a = %d, b = %d\n", a, b);
    printf("Is a == b? Result: %d\n", a == b); // 0 (false)
    printf("Is a != b? Result: %d\n", a != b); // 1 (true)
    printf("Is a > b?  Result: %d\n", a > b);  // 0 (false)
    printf("Is a <= b? Result: %d\n", a <= b); // 1 (true)

    // Pitfall demonstration
    int x = 1;
    if (x = 5) { // WARNING: This assigns 5 to x and is ALWAYS true!
        printf("\nThe value of x is now: %d. The if-statement was true!\n", x);
    }

    return 0;
}
```

---

### **3. Logical Operators**

These operators are used to combine or invert the results of relational expressions. They are fundamental to creating complex decision-making logic.

| Operator | Name | Description |
| :--- | :--- | :--- |
| `&&` | Logical AND | Returns `1` (true) only if **both** operands are true. |
| `||` | Logical OR | Returns `1` (true) if **at least one** of the operands is true. |
| `!` | Logical NOT | Inverts the state of its operand. Turns true to false (`0`) and false to true (`1`). |

#### **Short-Circuit Evaluation:**

C's logical operators use "short-circuiting," which is an important optimization:
*   For `expr1 && expr2`, if `expr1` is false, `expr2` is **never evaluated**.
*   For `expr1 || expr2`, if `expr1` is true, `expr2` is **never evaluated**.

This is useful for preventing errors, like in `if (pointer != NULL && pointer->member)`.

#### **C Code Example:**

```c
#include <stdio.h>

int main() {
    int age = 25;
    int hasLicense = 1; // 1 for true

    // Logical AND (&&)
    if (age > 18 && hasLicense == 1) {
        printf("You are eligible to drive.\n");
    }

    int isWeekend = 0; // 0 for false
    int isHoliday = 1; // 1 for true

    // Logical OR (||)
    if (isWeekend == 1 || isHoliday == 1) {
        printf("You don't have to work today!\n");
    }

    int isRaining = 0; // 0 for false

    // Logical NOT (!)
    if (!isRaining) { // !isRaining is the same as (isRaining == 0)
        printf("It is not raining, let's go outside.\n");
    }

    return 0;
}
```

---

### **4. Assignment Operators**

These operators are used to assign a value to a variable.

| Operator | Example | Equivalent To |
| :--- | :--- | :--- |
| `=` | `x = y` | `x = y` |
| `+=` | `x += y` | `x = x + y` |
| `-=` | `x -= y` | `x = x - y` |
| `*=` | `x *= y` | `x = x * y` |
| `/=` | `x /= y` | `x = x / y` |
| `%=` | `x %= y` | `x = x % y` |

The compound assignment operators (`+=`, `-=`, etc.) are convenient shorthand.

#### **C Code Example:**

```c
#include <stdio.h>

int main() {
    int score = 100;
    printf("Initial score: %d\n", score);

    score += 50; // score is now 100 + 50 = 150
    printf("Score after += 50: %d\n", score);

    score -= 20; // score is now 150 - 20 = 130
    printf("Score after -= 20: %d\n", score);

    score *= 2;  // score is now 130 * 2 = 260
    printf("Score after *= 2: %d\n", score);

    return 0;
}
```

---

### **5. Increment and Decrement Operators**

These operators are used to increase (`++`) or decrease (`--`) the value of an integer variable by exactly one. They have two forms: **prefix** and **postfix**.

*   **Prefix (`++var` or `--var`):** The variable is modified *first*, and the *new* value is used in the expression.
*   **Postfix (`var++` or `var--`):** The *original* value of the variable is used in the expression, and *then* the variable is modified.

| Operator | Name | Description |
| :--- | :--- | :--- |
| `++` | Increment | Increases integer value by one. |
| `--` | Decrement | Decreases integer value by one. |

#### **C Code Example:**

```c
#include <stdio.h>

int main() {
    int a = 10;
    int b = 10;

    printf("--- Prefix vs Postfix ---\n");
    printf("Initial values: a = %d, b = %d\n", a, b);

    // Prefix: Increment 'a' FIRST, then assign its new value (11) to 'prefix_a'
    int prefix_a = ++a;
    printf("After prefix_a = ++a:\n");
    printf("  prefix_a = %d\n", prefix_a); // 11
    printf("  a = %d\n\n", a);           // 11

    // Postfix: Assign 'b's original value (10) to 'postfix_b' FIRST, then increment 'b'
    int postfix_b = b++;
    printf("After postfix_b = b++:\n");
    printf("  postfix_b = %d\n", postfix_b); // 10
    printf("  b = %d\n", b);              // 11

    return 0;
}
```

---

### **6. Bitwise Operators**

These operators work on the individual bits (0s and 1s) of integer data. They are commonly used in low-level programming, such as controlling hardware or optimizing certain calculations.

| Operator | Name | Description |
| :--- | :--- | :--- |
| `&` | Bitwise AND | Sets each bit to 1 if both bits are 1. |
| `|` | Bitwise OR | Sets each bit to 1 if at least one of the two bits is 1. |
| `^` | Bitwise XOR | Sets each bit to 1 if only one of the two bits is 1. |
| `~` | Bitwise NOT (Complement) | Inverts all the bits. |
| `<<` | Left Shift | Shifts all bits to the left by a number of positions. |
| `>>` | Right Shift | Shifts all bits to the right by a number of positions. |

#### **C Code Example:**

```c
#include <stdio.h>

int main() {
    unsigned int a = 60; // In binary: 0011 1100
    unsigned int b = 13; // In binary: 0000 1101

    printf("a = %d (0011 1100)\n", a);
    printf("b = %d (0000 1101)\n\n", b);

    printf("a & b  = %d (0000 1100)\n", a & b);    // Result is 12
    printf("a | b  = %d (0011 1101)\n", a | b);    // Result is 61
    printf("a ^ b  = %d (0011 0001)\n", a ^ b);    // Result is 49
    printf("~a     = %u\n", ~a);                 // Inverts all bits, result is large
    printf("a << 2 = %d (1111 0000)\n", a << 2); // Result is 240
    printf("a >> 2 = %d (0000 1111)\n", a >> 2); // Result is 15

    return 0;
}
```

---

### **7. Miscellaneous Operators**

#### **`sizeof` Operator**
`sizeof` is a compile-time operator that returns the size, in bytes, of a variable or a data type.

#### **Conditional (Ternary) Operator (`? :`)**
This is a shorthand for an `if-else` statement.
**Syntax:** `condition ? expression_if_true : expression_if_false;`

#### **Address (`&`) and Indirection (`*`) Operators**
These are fundamental to pointers.
*   `&` (Address-of): Returns the memory address of a variable.
*   `*` (Dereference): Accesses the value stored at a memory address.

#### **C Code Example:**

```c
#include <stdio.h>

int main() {
    // --- sizeof Operator ---
    printf("Size of int: %zu bytes\n", sizeof(int));
    printf("Size of double: %zu bytes\n", sizeof(double));

    // --- Conditional (Ternary) Operator ---
    int age = 20;
    char* status = (age >= 18) ? "Adult" : "Minor";
    printf("\nAge %d is considered an %s.\n", age, status);

    // --- Address and Indirection ---
    int num = 100;
    int* ptr = &num; // 'ptr' now holds the memory address of 'num'

    printf("\nValue of num: %d\n", num);
    printf("Address of num: %p\n", &num);
    printf("Value stored in ptr (the address): %p\n", ptr);
    printf("Value at the address ptr points to: %d\n", *ptr); // Dereferencing

    return 0;
}
```

---

### **Operator Precedence and Associativity**

*   **Precedence:** Determines the order in which operators are evaluated in an expression with multiple operators. For example, `*` and `/` have higher precedence than `+` and `-`. `2 + 3 * 4` is evaluated as `2 + (3 * 4) = 14`.
*   **Associativity:** Determines the order in which operators with the *same precedence* are evaluated. It can be Left-to-Right or Right-to-Left. For example, `10 - 4 - 2` is evaluated as `(10 - 4) - 2 = 4` because subtraction is Left-to-Right.

#### **Simplified Precedence Table (Highest to Lowest)**

| Precedence | Operator | Description | Associativity |
| :--- | :--- | :--- | :--- |
| 1 | `()`, `[]` | Function call, array subscript | Left-to-Right |
| 2 | `++`, `--`, `!`, `~`, `*` (ptr) | Unary operators, Dereference | Right-to-Left |
| 3 | `*`, `/`, `%` | Multiplicative | Left-to-Right |
| 4 | `+`, `-` | Additive | Left-to-Right |
| 5 | `<<`, `>>` | Bitwise Shifts | Left-to-Right |
| 6 | `<`, `<=`, `>`, `>=` | Relational | Left-to-Right |
| 7 | `==`, `!=` | Equality | Left-to-Right |
| 8 | `&` | Bitwise AND | Left-to-Right |
| 9 | `^` | Bitwise XOR | Left-to-Right |
| 10 | `|` | Bitwise OR | Left-to-Right |
| 11 | `&&` | Logical AND | Left-to-Right |
| 12 | `||` | Logical OR | Left-to-Right |
| 13 | `?:` | Conditional (Ternary) | Right-to-Left |
| 14 | `=`, `+=`, `-=`, etc. | Assignment | Right-to-Left |

**Rule of thumb:** When in doubt, use parentheses `()` to explicitly control the order of evaluation. `(a + b) * c` is always clearer than relying on precedence rules.