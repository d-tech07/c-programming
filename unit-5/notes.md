Of course. Here are comprehensive notes for Unit 5: Arrays and Strings, designed for a 6-hour module. The notes include detailed theory, complete C code examples, and the exact output for each example.

---

### **Unit 5: Arrays and Strings (6 hrs)**

### **1. Introduction to Arrays**

#### **Theory**
Imagine you need to store the test scores of 100 students. You could declare 100 different variables: `score1`, `score2`, `score3`, ..., `score100`. This would be incredibly tedious and unmanageable.

An **array** solves this problem. An array is a collection of a fixed number of elements of the **same data type**, stored in a **contiguous block of memory**. Think of it as a row of labeled boxes, where each box holds the same kind of item and they are all lined up one after another.

**Key Characteristics of an Array:**
*   **Homogeneous:** All elements in an array must be of the same data type (e.g., all `int`, all `float`).
*   **Fixed Size:** The size of an array is determined at compile time and cannot be changed during program execution.
*   **Contiguous Memory:** The elements are stored next to each other in memory, which allows for efficient access.
*   **Indexed:** Each element has a unique index (or subscript) that identifies its position. **In C, array indexing is 0-based**, meaning the first element is at index 0, the second at index 1, and so on.

---

### **2. One-Dimensional Arrays**

#### **A. Declaration of an Array**

**Theory:**
To declare an array, you need to specify its data type, name, and size.

**Syntax:**
`data_type array_name[array_size];`

*   `data_type`: The type of elements the array will hold (e.g., `int`, `double`, `char`).
*   `array_name`: The name you give to your array.
*   `array_size`: A positive integer constant that specifies the number of elements in the array.

**Example:**
`int test_scores[30];` // Declares an array named 'test_scores' that can hold 30 integers.

#### **B. Initialization of Arrays**

**Theory:**
You can initialize an array at the time of its declaration by providing the initial values in a comma-separated list enclosed in curly braces `{}`.

**Method 1: Initializing with a specified size**
If you provide fewer initializers than the size of the array, the remaining elements are automatically initialized to zero.
```c
int marks[5] = {90, 85, 95}; // marks[0]=90, marks[1]=85, marks[2]=95, marks[3]=0, marks[4]=0
```

**Method 2: Initializing without a specified size**
The compiler will automatically calculate the size of the array based on the number of initializers.
```c
int numbers[] = {2, 4, 6, 8}; // Compiler automatically creates an array of size 4.
```

#### **C. Accessing Array Elements**

**Theory:**
You can access an individual element of an array using its index in square brackets `[]`. The valid range of indices for an array of size `N` is from `0` to `N-1`. Accessing an element outside this range (e.g., `array[N]`) is a common and serious bug called a **buffer overflow**, leading to undefined behavior.

**Code Example:**
This program declares an array, initializes it, accesses elements, and calculates the average of the scores.
```c
#include <stdio.h>

int main() {
    // Declare and initialize an array of 5 integer scores.
    int scores[5] = {88, 92, 79, 95, 84};
    int sum = 0;
    double average;

    // --- Accessing and Printing Individual Elements ---
    printf("The score at index 0 is: %d\n", scores[0]); // Access first element
    printf("The score at index 2 is: %d\n", scores[2]); // Access third element

    // --- Modifying an Element ---
    printf("\nChanging the score at index 2 from %d to 81.\n", scores[2]);
    scores[2] = 81;
    printf("The new score at index 2 is: %d\n", scores[2]);

    // --- Looping Through an Array to Calculate Sum ---
    // The for loop is perfect for iterating through an array.
    for (int i = 0; i < 5; i++) {
        sum = sum + scores[i]; // Add each score to the sum
    }

    // --- Calculating the Average ---
    // We cast the sum to a double to ensure floating-point division.
    average = (double)sum / 5;

    printf("\nThe sum of all scores is: %d\n", sum);
    printf("The average score is: %.2f\n", average);

    return 0;
}
```

**Output:**
```
The score at index 0 is: 88
The score at index 2 is: 79

Changing the score at index 2 from 79 to 81.
The new score at index 2 is: 81

The sum of all scores is: 440
The average score is: 88.00
```

---

### **3. Multidimensional Arrays**

#### **Theory**
A multidimensional array is an "array of arrays." The most common type is a **two-dimensional (2D) array**, which can be visualized as a grid or a table with rows and columns. They are useful for representing data like matrices, game boards, or tables of values.

**Declaration Syntax (2D Array):**
`data_type array_name[number_of_rows][number_of_columns];`

**Initialization Syntax (2D Array):**
You use nested curly braces, where each inner set of braces initializes one row.
`int matrix[2][3] = { {1, 2, 3}, {4, 5, 6} };`

This creates a 2x3 matrix:
Row 0: `1 2 3`
Row 1: `4 5 6`

**Accessing Elements:**
You need two indices: one for the row and one for the column. `matrix[row][col]`. To traverse a 2D array, you typically use nested `for` loops. The outer loop iterates through the rows, and the inner loop iterates through the columns of each row.

**Code Example:**
This program initializes a 2x3 matrix and prints its elements in a grid format.
```c
#include <stdio.h>

int main() {
    // Declare and initialize a 2D array (2 rows, 3 columns).
    int matrix[2][3] = {
        {10, 20, 30}, // Row 0
        {40, 50, 60}  // Row 1
    };

    printf("Displaying the 2x3 matrix:\n");

    // Outer loop for rows
    for (int i = 0; i < 2; i++) {
        // Inner loop for columns
        for (int j = 0; j < 3; j++) {
            // Access element at row i, column j
            printf("%d\t", matrix[i][j]);
        }
        // Print a newline after each row to format the output
        printf("\n");
    }

    return 0;
}
```

**Output:**
```
Displaying the 2x3 matrix:
10      20      30
40      50      60
```
*(Note: The spacing from `\t` might vary slightly depending on the terminal)*

---

### **4. Strings in C**

#### **Theory**
Unlike many modern languages, **C does not have a built-in string data type**. Instead, a string in C is a **convention**. By convention, a C-string is a **one-dimensional array of characters (`char`) that is terminated by a special character called the null character (`\0`)**.

This null terminator `\0` is crucial. It acts as a sentinel value that marks the end of the string. All standard string-handling functions (like `printf`, `strlen`) rely on this null character to know where the string ends.

**Example Visualization:**
The string "HELLO" is stored in memory as an array of 6 characters:
`'H' | 'E' | 'L' | 'L' | 'O' | '\0'`

**Initialization of Strings:**
**Method 1: Using a string literal (preferred)**
The compiler automatically adds the `\0` at the end.
```c
char greeting[] = "Hello"; // Creates an array of size 6.
```

**Method 2: Initializing as a character array**
You must manually add the `\0`.
```c
char greeting[] = {'H', 'e', 'l', 'l', 'o', '\0'};
```

#### **Reading Strings from the User**

**Problem with `scanf("%s", ...)`:**
`scanf("%s", ...)` is simple but has two major flaws:
1.  It stops reading at the first whitespace character (space, tab, newline). It cannot read a full name like "John Smith".
2.  It does not check the size of the array, which can lead to a dangerous **buffer overflow** if the user types more characters than the array can hold.

**The Safer Alternative: `fgets()`**
The `fgets()` function is the recommended way to read strings.

**Syntax:** `fgets(char *str, int size, FILE *stream);`
*   `str`: The character array where the string will be stored.
*   `size`: The maximum number of characters to read (including the null terminator). This prevents buffer overflows.
*   `stream`: The source to read from. For keyboard input, this is `stdin`.

**Key Point:** `fgets()` reads the newline character (`\n`) if there's room in the buffer. This often needs to be removed.

**Code Example:**
This program demonstrates the difference between `scanf` and `fgets`.
```c
#include <stdio.h>

int main() {
    char name_scanf[20];
    char name_fgets[20];

    // --- Using scanf (Problematic) ---
    printf("Enter your full name (using scanf): ");
    scanf("%s", name_scanf); // Try typing "Ada Lovelace"
    printf("Hello, %s!\n\n", name_scanf);

    // --- Using fgets (Recommended) ---
    // We need to clear the input buffer from the previous scanf
    // This reads and discards characters until a newline is found
    while(getchar() != '\n'); 

    printf("Enter your full name again (using fgets): ");
    fgets(name_fgets, 20, stdin); // Reads the entire line
    printf("Hello, %s", name_fgets); // Prints the string with the newline

    return 0;
}
```

**Output (Sample Run):**
```
Enter your full name (using scanf): Ada Lovelace
Hello, Ada!

Enter your full name again (using fgets): Ada Lovelace
Hello, Ada Lovelace
```
*(Notice how `scanf` only read "Ada", while `fgets` read the full name and the newline character, which caused the cursor to move to the next line after printing.)*

---

### **5. Functions Related to Strings**

To work with strings, C provides a rich library of functions in the `<string.h>` header file. You must include this header to use them: `#include <string.h>`

Here are some of the most common ones:

#### **A. `strlen()` - String Length**
*   **Purpose:** Calculates the length of a string, **not including** the null terminator `\0`.
*   **Syntax:** `size_t strlen(const char *str);` (`size_t` is an unsigned integer type)

**Code Example:**
```c
#include <stdio.h>
#include <string.h>

int main() {
    char my_string[] = "C Programming";
    int length = strlen(my_string);
    printf("The string is: \"%s\"\n", my_string);
    printf("Its length is: %d characters.\n", length);
    return 0;
}
```
**Output:**
```
The string is: "C Programming"
Its length is: 13 characters.
```

#### **B. `strcpy()` - String Copy**
*   **Purpose:** Copies a string from a source to a destination.
*   **Syntax:** `char* strcpy(char *destination, const char *source);`
*   **Warning:** The destination array must be large enough to hold the source string, including its `\0`.

**Code Example:**
```c
#include <stdio.h>
#include <string.h>

int main() {
    char source[] = "Hello World!";
    char destination[20]; // Must be large enough

    strcpy(destination, source);

    printf("Source string: %s\n", source);
    printf("Destination string after copy: %s\n", destination);
    return 0;
}
```
**Output:**
```
Source string: Hello World!
Destination string after copy: Hello World!
```

#### **C. `strcat()` - String Concatenation**
*   **Purpose:** Appends the source string to the end of the destination string.
*   **Syntax:** `char* strcat(char *destination, const char *source);`
*   **Warning:** The destination array must be large enough to hold its own content PLUS the source string's content and the final `\0`.

**Code Example:**
```c
#include <stdio.h>
#include <string.h>

int main() {
    char first_name[20] = "John"; // Needs space for the last name
    char last_name[] = " Doe";

    strcat(first_name, last_name); // Appends " Doe" to "John"

    printf("Full name: %s\n", first_name);
    return 0;
}
```
**Output:**
```
Full name: John Doe
```

#### **D. `strcmp()` - String Comparison**
*   **Purpose:** Compares two strings lexicographically (like in a dictionary). It is case-sensitive.
*   **Syntax:** `int strcmp(const char *str1, const char *str2);`
*   **Return Value:**
    *   `0` if `str1` and `str2` are identical.
    *   `< 0` (a negative value) if `str1` comes before `str2` alphabetically.
    *   `> 0` (a positive value) if `str1` comes after `str2` alphabetically.

**Code Example:**
```c
#include <stdio.h>
#include <string.h>

int main() {
    char str1[] = "Apple";
    char str2[] = "Banana";
    char str3[] = "Apple";

    // Compare str1 and str2
    int result1 = strcmp(str1, str2);
    if (result1 == 0) {
        printf("\"%s\" and \"%s\" are identical.\n", str1, str2);
    } else {
        printf("\"%s\" and \"%s\" are NOT identical. Result: %d\n", str1, str2, result1);
    }

    // Compare str1 and str3
    int result2 = strcmp(str1, str3);
    if (result2 == 0) {
        printf("\"%s\" and \"%s\" are identical.\n", str1, str3);
    } else {
        printf("\"%s\" and \"%s\" are NOT identical. Result: %d\n", str1, str3, result2);
    }
    return 0;
}
```
**Output:**
```
"Apple" and "Banana" are NOT identical. Result: -1
"Apple" and "Apple" are identical.
```
*(The exact non-zero result can vary, but its sign—negative or positive—is guaranteed.)*