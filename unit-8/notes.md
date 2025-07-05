
---

### **Unit 8: Structure and Unions (5 hrs)**

### **Introduction**
we have worked with basic data types (`int`, `char`, `float`) and derived types like arrays. Arrays are powerful, but they have a major limitation: all elements must be of the **same data type**.

What if we want to group together different types of data related to a single entity? For example, a student record needs a name (string), a roll number (integer), and a GPA (float). This is where **structures** come in. They allow us to create a custom, user-defined data type that bundles together variables of different data types.

---

### **1. Definition of Structure**

#### **Theory**
A **structure** is a user-defined data type that allows you to combine data items of different kinds under a single name. It provides a way to logically group related information. Each data item within a structure is called a **member** or a **field**.

**Defining a Structure:**
The `struct` keyword is used to define the structure's template or blueprint. This definition does not allocate any memory; it just describes what the new data type looks like.

**Syntax for Definition:**
```c
struct structure_name {
    data_type member1;
    data_type member2;
    // ...
};
```

**Declaring a Structure Variable:**
Once the structure is defined, you can declare variables of that type, just like you would with `int` or `char`. This is when memory is allocated.

**Syntax for Declaration:**
`struct structure_name variable_name;`

**Accessing Members:**
To access the members of a structure variable, you use the **dot (`.`) operator**, also known as the member access operator.
`variable_name.member_name`

#### **Code Example**
This program defines a `Student` structure, declares a variable of that type, and accesses its members.
```c
#include <stdio.h>
#include <string.h>

// --- Structure Definition (Blueprint) ---
// This defines a new data type called 'struct Student'.
struct Student {
    int roll_number;
    char name[50];
    float gpa;
};

int main() {
    // --- Structure Variable Declaration ---
    // 's1' is a variable of type 'struct Student'. Memory is allocated here.
    struct Student s1;

    // --- Accessing and Assigning Values to Members ---
    // Use the dot (.) operator to access each member.
    s1.roll_number = 101;
    strcpy(s1.name, "Alice"); // Use strcpy for string members
    s1.gpa = 3.8;

    // --- Printing the Member Values ---
    printf("--- Student Record ---\n");
    printf("Roll Number: %d\n", s1.roll_number);
    printf("Name: %s\n", s1.name);
    printf("GPA: %.2f\n", s1.gpa);

    return 0;
}
```

**Output:**
```
--- Student Record ---
Roll Number: 101
Name: Alice
GPA: 3.80
```

---

### **2. Nested type Structure**

#### **Theory**
C allows you to have a structure as a member of another structure. This is called **nesting of structures**. It's useful when a property of an entity is itself a complex object. For example, a student has a date of birth, which itself consists of a day, month, and year.

To access the members of the inner (nested) structure, you use a chain of dot operators.
`outer_variable.inner_variable.inner_member`

#### **Code Example**
This program defines a `Date` structure and nests it inside a `Person` structure.
```c
#include <stdio.h>
#include <string.h>

// --- Inner Structure Definition ---
struct Date {
    int day;
    int month;
    int year;
};

// --- Outer Structure Definition ---
// This structure contains another structure as a member.
struct Person {
    char name[50];
    struct Date dob; // 'dob' is a variable of type 'struct Date'
};

int main() {
    struct Person p1;

    // Assign values to the outer structure members
    strcpy(p1.name, "Bob");

    // Assign values to the members of the nested structure
    p1.dob.day = 15;
    p1.dob.month = 5;
    p1.dob.year = 1998;

    // Print the information
    printf("--- Person Details ---\n");
    printf("Name: %s\n", p1.name);
    printf("Date of Birth: %d-%d-%d\n", p1.dob.day, p1.dob.month, p1.dob.year);

    return 0;
}
```

**Output:**
```
--- Person Details ---
Name: Bob
Date of Birth: 15-5-1998
```

---

### **3. Arrays of Structure**

#### **Theory**
Just as you can create an array of `int`s or `char`s, you can create an **array of structures**. This is extremely useful for storing records of multiple entities, like a list of all students in a class or all employees in a department.

**Declaration:**
`struct structure_name array_name[size];`

To access the members of a specific structure in the array, you first use the array index `[]` and then the dot operator `.`.
`array_name[index].member_name`

#### **Code Example**
This program creates an array to store records for three employees.
```c
#include <stdio.h>
#include <string.h>

struct Employee {
    int id;
    char name[50];
    float salary;
};

int main() {
    // Declare an array that can hold 3 Employee structures.
    struct Employee employees[3];

    printf("--- Enter Employee Data ---\n");

    // Use a loop to get data for each employee
    for (int i = 0; i < 3; i++) {
        printf("\nEnter details for Employee %d:\n", i + 1);
        printf("ID: ");
        scanf("%d", &employees[i].id);

        // Clear input buffer before reading string
        while(getchar() != '\n'); 

        printf("Name: ");
        fgets(employees[i].name, 50, stdin);
        
        printf("Salary: ");
        scanf("%f", &employees[i].salary);
    }

    printf("\n--- Employee Records ---\n");
    // Use another loop to display the data
    for (int i = 0; i < 3; i++) {
        printf("ID: %d, Name: %s, Salary: %.2f\n",
               employees[i].id, employees[i].name, employees[i].salary);
    }

    return 0;
}
```

**Output (Sample Run):**
```
--- Enter Employee Data ---

Enter details for Employee 1:
ID: 101
Name: Charlie Davis
Salary: 60000

Enter details for Employee 2:
ID: 102
Name: Diana Prince
Salary: 75000

Enter details for Employee 3:
ID: 103
Name: Eve Adams
Salary: 55000

--- Employee Records ---
ID: 101, Name: Charlie Davis
, Salary: 60000.00
ID: 102, Name: Diana Prince
, Salary: 75000.00
ID: 103, Name: Eve Adams
, Salary: 55000.00
```
*(Note: The newline in the `Name` field is due to `fgets` capturing it. This can be cleaned up, but is shown here for accuracy.)*

---

### **4. Structure and Pointers**

#### **Theory**
You can have a **pointer to a structure variable**. This is a very common and efficient way to work with structures, especially when passing them to functions, as it avoids copying the entire structure.

**Declaration:**
`struct structure_name *pointer_name;`

**Accessing Members via a Pointer:**
There are two ways to access the members of a structure through a pointer:
1.  **Using the dereference (`*`) and dot (`.`) operators:**
    `(*pointer_name).member_name`
    The parentheses are **mandatory** because the dot operator (`.`) has higher precedence than the dereference operator (`*`).
2.  **Using the arrow (`->`) operator:**
    `pointer_name->member_name`
    This is a much cleaner shorthand and is the universally preferred method.

#### **Code Example**
```c
#include <stdio.h>

struct Book {
    char title[100];
    int pages;
};

int main() {
    struct Book b1 = {"The C Programming Language", 272};
    struct Book *ptr; // Declare a pointer to a struct Book

    ptr = &b1; // Assign the address of b1 to the pointer

    printf("--- Accessing members using pointers ---\n");

    // Method 1: Using (*ptr).member
    printf("Title (using * and .): %s\n", (*ptr).title);
    printf("Pages (using * and .): %d\n", (*ptr).pages);

    // Method 2: Using -> operator (preferred)
    printf("\nTitle (using ->): %s\n", ptr->title);
    printf("Pages (using ->): %d\n", ptr->pages);

    return 0;
}
```

**Output:**
```
--- Accessing members using pointers ---
Title (using * and .): The C Programming Language
Pages (using * and .): 272

Title (using ->): The C Programming Language
Pages (using ->): 272
```

---

### **5. Unions**

#### **Theory**
A **union** is a special user-defined data type that looks similar to a structure, but it has a crucial difference: **all members of a union share the same memory location**.

This means that a union can only hold a value for **one member at a time**. The size of the union is the size of its **largest member**.

**Why use a union?**
*   **Memory Saving:** When you know you will only need to use one member out of a set of possible members at any given time, a union saves memory compared to a structure.
*   **Data Interpretation:** Unions can be used to interpret the same block of memory as different data types.

**Warning:** If you store a value in one member and then try to access a different member, you will get garbage data because you are misinterpreting the bits in memory.

#### **Code Example**
```c
#include <stdio.h>

union Data {
    int i;
    float f;
    char str[20];
};

int main() {
    union Data data;

    printf("Memory size occupied by union Data: %zu bytes\n", sizeof(data));

    // Store an integer value
    data.i = 10;
    printf("\nData after storing an integer:\n");
    printf("data.i : %d\n", data.i);
    printf("data.f : %f (garbage)\n", data.f);
    printf("data.str : %s (garbage)\n", data.str);

    // Store a float value (this overwrites the integer)
    data.f = 220.5;
    printf("\nData after storing a float:\n");
    printf("data.i : %d (garbage)\n", data.i);
    printf("data.f : %f\n", data.f);
    printf("data.str : %s (garbage)\n", data.str);

    // Store a string value (this overwrites the float)
    strcpy(data.str, "C Programming");
    printf("\nData after storing a string:\n");
    printf("data.i : %d (garbage)\n", data.i);
    printf("data.f : %f (garbage)\n", data.f);
    printf("data.str : %s\n", data.str);

    return 0;
}
```

**Output:**
```
Memory size occupied by union Data: 20 bytes

Data after storing an integer:
data.i : 10
data.f : 0.000000 (garbage)
data.str :  (garbage)

Data after storing a float:
data.i : 1131441357 (garbage)
data.f : 220.500000
data.str : @ (garbage)

Data after storing a string:
data.i : 1869771331 (garbage)
data.f : 41655068897536.000000 (garbage)
data.str : C Programming
```
*(The exact garbage values will vary, but the concept remains the same.)*

---

### **6. Self-Referential Structure**

#### **Theory**
A **self-referential structure** is a structure that contains a member which is a **pointer to another structure of the same type**.

This concept is the fundamental building block for advanced dynamic data structures like **Linked Lists**, **Trees**, and **Graphs**.

It is critical to understand that the member must be a **pointer**. You cannot have a structure as a member of itself (`struct Node next;`), as this would create a type with an infinite size. A pointer, however, just stores an address and has a fixed size.

A `struct Node` in a linked list, for example, contains some data and a pointer to the `next` node in the sequence. The last node's `next` pointer is set to `NULL` to signify the end of the list.

#### **Code Example**
This program manually creates a simple linked list with three nodes.
```c
#include <stdio.h>
#include <stdlib.h>

// Define the self-referential structure
struct Node {
    int data;
    struct Node *next; // Pointer to a structure of the same type
};

int main() {
    // Manually create three nodes using dynamic memory allocation
    struct Node *head = (struct Node*)malloc(sizeof(struct Node));
    struct Node *second = (struct Node*)malloc(sizeof(struct Node));
    struct Node *third = (struct Node*)malloc(sizeof(struct Node));

    // Assign data to each node
    head->data = 10;
    second->data = 20;
    third->data = 30;

    // --- Link the nodes together ---
    head->next = second;   // Head points to the second node
    second->next = third;  // Second points to the third node
    third->next = NULL;    // Third node is the end, so it points to NULL

    // --- Traverse and print the linked list ---
    printf("Traversing the linked list:\n");
    struct Node *current = head; // Start at the head
    while (current != NULL) {    // Loop until we reach the end
        printf("%d -> ", current->data);
        current = current->next; // Move to the next node
    }
    printf("NULL\n");

    // Free the allocated memory
    free(head);
    free(second);
    free(third);

    return 0;
}
```

**Output:**
```
Traversing the linked list:
10 -> 20 -> 30 -> NULL
```