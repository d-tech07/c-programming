
---

### **Unit 9: Files and File Handling in C (4 hrs)**

### **Introduction to File Handling**

#### **Theory**
Any data our programs have worked with (like variables, arrays, etc.) has been stored in RAM (Random Access Memory). RAM is **volatile**, meaning all data is lost when the program ends or the computer is turned off.

To store data permanently, we need to save it to a **file** on a non-volatile storage device like a hard drive, SSD, or USB stick. **File handling** in C is the mechanism that allows us to create, read, write, and update these files from within our program.

**What is a Stream?**
C views a file as a continuous sequence or **stream** of bytes. It uses a concept called a "stream" to provide a consistent interface for I/O (Input/Output) operations, whether they are with a file on disk or with the console (keyboard/screen).
*   `stdin`: The standard input stream (usually the keyboard).
*   `stdout`: The standard output stream (usually the screen).
*   `stderr`: The standard error stream (usually the screen).

**The `FILE` Pointer:**
To work with a file, you must use a special type of pointer called a **`FILE` pointer**. This pointer, defined in the `<stdio.h>` library, acts as a link between your program and the file on the disk. It holds all the information needed to manage the file stream, such as its current position, whether an error has occurred, etc.

**The Basic Process of File Handling:**
1.  Declare a `FILE` pointer.
2.  **Open** a file using the `fopen()` function. This associates the `FILE` pointer with a specific disk file.
3.  **Perform** I/O operations (read, write) using functions like `fprintf()`, `fscanf()`, `fgetc()`, `fputc()`, etc.
4.  **Close** the file using the `fclose()` function. This is a critical step to save all changes and release the file from your program's control.

---

### **Operating a File in Different Modes**

#### **Theory**
When you open a file with `fopen()`, you must specify a **mode**. The mode tells C what you intend to do with the file (read, write, or append).

**The `fopen()` Function:**
*   **Syntax:** `FILE *fopen(const char *filename, const char *mode);`
*   **Parameters:**
    *   `filename`: A string containing the name of the file (e.g., `"data.txt"`).
    *   `mode`: A string specifying the file access mode.
*   **Return Value:**
    *   On success, it returns a `FILE` pointer to the opened file.
    *   On failure (e.g., file not found in read mode, no disk space), it returns `NULL`. **You must always check for `NULL` to handle errors.**

**Common File Modes:**

| Mode | Meaning | Behavior if File Exists | Behavior if File Does Not Exist |
| :--- | :--- | :--- | :--- |
| **`"r"`** | **Read** | Opens the file for reading. File pointer is at the beginning. | **Fails.** `fopen()` returns `NULL`. |
| **`"w"`** | **Write** | **Destroys (truncates)** the content and opens for writing. | **Creates** a new, empty file. |
| **`"a"`** | **Append** | Opens for writing. File pointer is at the **end**. Content is preserved. | **Creates** a new, empty file. |
| **`"r+"`** | Read & Write | Opens for reading and writing. File pointer is at the beginning. | **Fails.** `fopen()` returns `NULL`. |
| **`"w+"`** | Read & Write | **Destroys** the content and opens for reading and writing. | **Creates** a new, empty file. |
| **`"a+"`** | Read & Append | Opens for reading and appending. Reading starts at the beginning, writing happens at the end. | **Creates** a new, empty file. |

*Note: You can add `b` to any mode (e.g., `"rb"`, `"wb"`) to open the file in **binary mode**, which is used for non-text files like images or executables.*

---

### **Creating and Operating a File in Write (`"w"`) Mode**

#### **Theory**
Using `"w"` mode is for writing data from scratch. If the file `notes.txt` already exists, its contents will be completely erased. If it doesn't exist, it will be created.

**Key Functions for Writing:**
*   `fprintf(FILE *stream, const char *format, ...)`: Writes formatted output to a file, just like `printf` does to the console.
*   `fputc(int character, FILE *stream)`: Writes a single character to the file.
*   `fputs(const char *str, FILE *stream)`: Writes a string to the file (does not add a newline).

#### **Code Example**
```c
#include <stdio.h>

int main() {
    // 1. Declare a FILE pointer
    FILE *file_ptr;

    // 2. Open the file in write mode ("w")
    // This will create 'notes.txt' or overwrite it if it exists.
    file_ptr = fopen("notes.txt", "w");

    // 3. ALWAYS check if the file opened successfully
    if (file_ptr == NULL) {
        printf("Error! Could not open or create the file.\n");
        return 1; // Exit with an error
    }

    // 4. Perform write operations
    printf("File opened successfully. Writing content...\n");
    fprintf(file_ptr, "This is line 1.\n");
    fputs("This is line 2.\n", file_ptr);
    fputc('T', file_ptr);
    fputc('h', file_ptr);
    fputc('i', file_ptr);
    fputc('s', file_ptr);
    fputc(' ', file_ptr);
    fputc('i', file_ptr);
    fputc('s', file_ptr);
    fputc(' ', file_ptr);
    fputc('l', file_ptr);
    fputc('i', file_ptr);
    fputc('n', file_ptr);
    fputc('e', file_ptr);
    fputc(' ', file_ptr);
    fputc('3', file_ptr);
    fputc('.', file_ptr);
    fputc('\n', file_ptr);

    // 5. Close the file to save changes
    fclose(file_ptr);

    printf("Content written to 'notes.txt' and file closed.\n");

    return 0;
}
```

**Output (on the console):**
```
File opened successfully. Writing content...
Content written to 'notes.txt' and file closed.
```

**Result (content of the created `notes.txt` file):**
```
This is line 1.
This is line 2.
This is line 3.
```

---

### **Operating a File in Read (`"r"`) Mode**

#### **Theory**
Using `"r"` mode is for reading data from an existing file. If the file does not exist, `fopen()` will fail and return `NULL`.

**Key Functions for Reading:**
*   `fscanf(FILE *stream, const char *format, ...)`: Reads formatted input from a file, just like `scanf`.
*   `fgetc(FILE *stream)`: Reads a single character from the file. Returns `EOF` (End Of File) when there are no more characters to read.
*   `fgets(char *str, int n, FILE *stream)`: Reads a line of text (up to `n-1` characters) from the file. Returns `NULL` at the end of the file.

#### **Code Example**
This program reads the `notes.txt` file we just created.
```c
#include <stdio.h>

int main() {
    FILE *file_ptr;
    char buffer[255]; // A buffer to store a line of text

    // Open the file in read mode ("r")
    file_ptr = fopen("notes.txt", "r");

    // Check if the file exists and was opened
    if (file_ptr == NULL) {
        printf("Error! Could not open 'notes.txt' for reading. Does it exist?\n");
        return 1;
    }

    printf("File 'notes.txt' opened. Reading content:\n\n");

    // Read the file line by line using fgets
    // fgets returns NULL when it reaches the end of the file.
    while (fgets(buffer, 255, file_ptr) != NULL) {
        // Print the line we just read from the buffer
        printf("%s", buffer);
    }

    // Close the file
    fclose(file_ptr);

    printf("\n\nFinished reading and file closed.\n");

    return 0;
}
```

**Output (on the console):**
```
File 'notes.txt' opened. Reading content:

This is line 1.
This is line 2.
This is line 3.


Finished reading and file closed.
```

---

### **Creating and Operating a File in Append (`"a"`) Mode**

#### **Theory**
Using `"a"` mode is for adding new data to the **end** of an existing file without deleting its current contents. If the file doesn't exist, it will be created, just like with `"w"` mode.

#### **Code Example**
This program adds more content to our existing `notes.txt` file.
```c
#include <stdio.h>

int main() {
    FILE *file_ptr;

    // Open the file in append mode ("a")
    file_ptr = fopen("notes.txt", "a");

    // Check for errors
    if (file_ptr == NULL) {
        printf("Error! Could not open file for appending.\n");
        return 1;
    }

    printf("File opened successfully. Appending new content...\n");

    // The file pointer is now at the end of the file.
    // New writes will be added after the existing content.
    fprintf(file_ptr, "This is a new line added in append mode.\n");
    fputs("This is the final line.\n", file_ptr);

    // Close the file
    fclose(file_ptr);

    printf("Content appended and file closed.\n");

    return 0;
}
```

**Output (on the console):**
```
File opened successfully. Appending new content...
Content appended and file closed.
```

**Result (new content of the `notes.txt` file):**
```
This is line 1.
This is line 2.
This is line 3.
This is a new line added in append mode.
This is the final line.
```

---

### **A Complete Example: Saving and Reading Structured Data**

This example demonstrates a practical use case: saving student records (structures) to a file and then reading them back.

#### **Code Example**
```c
#include <stdio.h>

// Define a simple structure for a student
struct Student {
    char name[50];
    int id;
    float gpa;
};

int main() {
    struct Student s_write1 = {"Alice", 101, 3.8};
    struct Student s_write2 = {"Bob", 102, 3.5};
    struct Student s_read; // A variable to hold data read from the file
    FILE *file_ptr;

    // --- STEP 1: Write structured data to a file ---
    file_ptr = fopen("students.dat", "w");
    if (file_ptr == NULL) {
        printf("Error creating file.\n");
        return 1;
    }
    printf("Writing records to students.dat...\n");
    // Use fprintf for formatted writing
    fprintf(file_ptr, "%s %d %.2f\n", s_write1.name, s_write1.id, s_write1.gpa);
    fprintf(file_ptr, "%s %d %.2f\n", s_write2.name, s_write2.id, s_write2.gpa);
    fclose(file_ptr);
    printf("Done writing.\n\n");

    // --- STEP 2: Read structured data from the file ---
    file_ptr = fopen("students.dat", "r");
    if (file_ptr == NULL) {
        printf("Error reading file.\n");
        return 1;
    }
    printf("Reading records from students.dat:\n");
    // Use fscanf in a loop. It returns the number of items successfully read.
    // We expect to read 3 items (name, id, gpa) on each line.
    while (fscanf(file_ptr, "%s %d %f", s_read.name, &s_read.id, &s_read.gpa) == 3) {
        printf("  - Name: %s, ID: %d, GPA: %.2f\n", s_read.name, s_read.id, s_read.gpa);
    }
    fclose(file_ptr);
    printf("Done reading.\n");

    return 0;
}
```

**Output (on the console):**
```
Writing records to students.dat...
Done writing.

Reading records from students.dat:
  - Name: Alice, ID: 101, GPA: 3.80
  - Name: Bob, ID: 102, GPA: 3.50
Done reading.
```

**Result (content of the created `students.dat` file):**
```
Alice 101 3.80
Bob 102 3.50
```