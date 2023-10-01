
# Training Schedule Week 5: Introduction to C Programming

## Sunday:

### Introduction to C Programming:

- Understanding the C programming language.
- Differentiating between C and C++.
- Reasons to use C for programming.
- Start the course "Advanced C Programming Course on Udemy."


## Monday:

### Basic Operations in C:

- Arithmetic Operations in C. (+ , - , * , / , % , ++ , -- )
- Logical Operations in C. (&& , || , ! ) any non zero = true, zero is false.
- Introduction to Loops: 'for' and 'while' loops:
```c
for(initialization; condition; update)
{
    // loop body
}
while(condition)
{
    // loop body
}
```
- Exploring Bitwise Operators in C:
```c
int result = 5 & 3;  // result is 1 (binary: 0101 & 0011 = 0001)
int result = 5 | 3;  // result is 7 (binary: 0101 | 0011 = 0111)
int result = 5 ^ 3;  // result is 6 (binary: 0101 ^ 0011 = 0110)
int result = ~5;     // result is -6 on a system using two's complement for negative numbers
int result = 5 << 1; // result is 10 (binary: 0101 << 1 = 1010)
int result = 5 >> 1; // result is 2 (binary: 0101 >> 1 = 0010)
```
- When working with bitwise operations, especially shifts, it's essential to be cautious with signed integers. In some cases, using an unsigned integer type (unsigned int, for instance) can help avoid unexpected behaviors.
- Start working on the C project "word searcher":
  - Read file: Read a book and count how many times each word occurred (option to write it in increasing or decreasing order).
  - Write a report of the top 10 words.
  - Ability to search for the occurrence of a specific word.


## Tuesday:

### Data Types in C:

- Primary Data Types in C (Integer, Character, Double, Floating-point, Void):
  - **Integer (int):**
    - Used to store integer values.
    - The size of int can vary based on the architecture, but it's usually either 2 bytes (16 bits) or 4 bytes (32 bits).
    - There are several modifiers that can be applied to int to adjust its size and signedness:
      - short int or short: At least 2 bytes.
      - long int or long: At least 4 bytes, but on many modern systems, it's 8 bytes (64 bits).
      - long long int or long long: At least 8 bytes.
      - unsigned: This modifier can be combined with int and its variations to denote that the integer type should only hold non-negative values.
  
- **Character (char):**
  - Used to store a single character.
  - Occupies 1 byte of memory (usually 8 bits).
  - Can store values from -128 to 127 for signed char and 0 to 255 for unsigned char.
  - Can be used to perform integer arithmetic since, at its core, it represents integer values corresponding to character encodings (like ASCII).
  
- **Double (double):**
  - Used to store double-precision floating-point numbers.
  - Usually occupies 8 bytes (64 bits) of memory.
  - Offers more precision and a larger range than float.
  
- **Floating-point (float):**
  - Used to store single-precision floating-point numbers.
  - Occupies 4 bytes (32 bits) of memory.
  - Suitable for decimal numbers, but due to the way floating-point arithmetic works, not all decimal numbers can be represented exactly.
  
- **Void (void):**
  - It is not really a data type in the same sense as the above. Instead, void represents the absence of value.
  - Commonly used to indicate functions that don't return a value.
  - Can also be used for pointers to indicate a generic pointer type (void*).
  
  ```c
  void myFunction() {
      // This function does not return a value.
  }
  ```
  
  Remember, the exact size and range of these data types can vary depending on the architecture and compiler. It's always a good practice to use the `sizeof` operator if you need to find the size of a data type for a particular platform. Furthermore, in cases where exact sizes are crucial, the C standard library provides a header `<stdint.h>` which offers fixed-width integer types like `int32_t` and `uint64_t`.


- Modifiers in C: 'signed,' 'unsigned,' 'short,' 'long,' etc:

1. **`signed`:**
   - By default, the `int` and `char` data types are signed, meaning they can hold both positive and negative values.
   - The `signed` modifier explicitly declares a data type as signed. However, it's not commonly used because the default behavior is usually sufficient.
   - Example:
     ```c
     signed int s_num = -123;
     signed char s_char = -65;
     ```

2. **`unsigned`:**
   - The `unsigned` modifier indicates that a data type can only hold non-negative values. As a result, the positive range is doubled compared to its signed counterpart.
   - Most commonly used with `int` and `char`, but can also be used with `short` and `long`.
   - Example:
     ```c
     unsigned int u_num = 123;
     unsigned char u_char = 65;
     ```

3. **`short`:**
   - Used to specify a shorter version of an integer.
   - Typically, a `short int` or simply `short` takes up 2 bytes of memory, but this can vary based on the architecture.
   - Example:
     ```c
     short sh_num = 32767;    // On many systems, the maximum value for a signed short
     unsigned short u_sh_num = 65535;  // Maximum value for an unsigned short on many systems
     ```

4. **`long`:**
   - Specifies a longer integer type.
   - On many systems, a `long int` or simply `long` takes up 4 bytes of memory, the same as a regular `int`. However, on some systems (especially 64-bit systems), it might occupy 8 bytes.
   - Can also be used with `double` to specify extended precision.
   - Example:
     ```c
     long lg_num = 123456789L;
     unsigned long u_lg_num = 123456789UL;
     long double ld_value = 3.141592653589793238L;
     ```

5. **`long long`:**
   - This is an extension to the `long` modifier to specify even longer integers, especially for 64-bit integer support.
   - A `long long int` or simply `long long` typically takes up 8 bytes of memory.
   - Example:
     ```c
     long long ll_num = 9223372036854775807LL;    // Maximum value for a signed long long on many systems
     unsigned long long u_ll_num = 18446744073709551615ULL;  // Maximum value for an unsigned long long on many systems
     ```

Also:

**Storage Class Specifiers:**

- `auto`: Default storage class for local variables. Rarely used explicitly.
- `register`: Suggests that the variable be stored in a CPU register, if possible. However, modern compilers often make better decisions regarding register allocation without this hint.
- `static`: Retains the variable's value between function invocations or restricts the variable's visibility to its translation unit.
- `extern`: Indicates that the variable is declared, but defined elsewhere, possibly in another source file.

**Type Specifiers:**

- Basic Types: `int`, `char`, `float`, `double`, `void`.
- Modifiers: `short`, `long`, `signed`, `unsigned`, `long long` (as mentioned before).
- `_Bool`: A boolean type introduced in C99.
- `_Complex` and `_Imaginary`: Complex number types introduced in C99. They're not commonly used in everyday programming.


**Type Qualifiers:**

- `const`: Indicates the variable's value cannot be changed after initialization.
- `volatile`: Informs the compiler that a variable can be changed at any time, without any action being taken by the code the compiler finds. It is often used in low-level programming, such as when interfacing with hardware.
- `restrict`: A pointer qualifier introduced in C99, which tells the compiler that the pointer is the only means to access the object it points to during its lifetime.

**Function Specifiers (C11 onwards):**

- `_Noreturn`: Indicates that a function does not return.
- `_Generic`: Introduces generic selection, which is a way to perform compile-time type selection.

**Alignment Specifier (C11 onwards):**

- `_Alignas`: Specifies the alignment requirement of a variable or type.

**Atomic Type Qualifier (C11 onwards):**

- `_Atomic`: Used for atomic types, which are types for which the C standard provides atomic operations.


### Working with Strings in C:

In C, strings are essentially arrays of characters terminated by a null character (`'\0'`). Since C does not have built-in support for strings as a primary data type, like some other languages do, they are manipulated using character arrays and a set of standard library functions provided by the `<string.h>` header.

Here's an overview of working with strings in C:

1. **String Initialization**:
    - Using a string literal:
      ```c
      char str[] = "Hello, world!";
      ```
    - Specifying size:
      ```c
      char str[50] = "Hello";
      ```
    - Without specifying size:
      ```c
      char str[] = {'H', 'e', 'l', 'l', 'o', '\0'};
      ```

2. **String Input/Output**:
    - `printf` and `scanf` from the `<stdio.h>` header are commonly used.
      ```c
      char str[50];
      printf("Enter a string: ");
      scanf("%49s", str);  // Reads a string until whitespace
      ```
    - For reading a line (including spaces):
      ```c
      fgets(str, sizeof(str), stdin);
      ```


3. **String Functions (`<string.h>`)**:
    - `strlen(str)`: Returns the length of the string.
    - `strcpy(dest, src)`: Copies the string `src` to `dest`.
    - `strcat(dest, src)`: Concatenates the string `src` onto the end of `dest`.
    - `strcmp(str1, str2)`: Compares two strings. Returns 0 if they're equal, a negative value if `str1` is lexicographically less than `str2`, or a positive value if it's greater.
    - `strncpy(dest, src, n)`: Copies up to `n` characters from the string `src` to `dest`.
    - `strncat(dest, src, n)`: Concatenates up to `n` characters of string `src` to the end of `dest`.
    - `strncmp(str1, str2, n)`: Compares up to `n` characters of two strings.

4. **String Manipulation**:
   - You can iterate through a string using a loop until the null terminator is found.
   - Example – to convert a string to uppercase:
     ```c
     for(int i = 0; str[i]; i++) {
         str[i] = toupper(str[i]);
     }
     ```
     Note: `toupper()` is a function from the `<ctype.h>` header.

5. **String-to-Number Conversions**:
    - `atoi(str)`: Converts a string to an integer.
    - `atol(str)`: Converts a string to a long integer.
    - `atof(str)`: Converts a string to a floating-point number.
    - For more control, `strtol`, `strtoul`, `strtod`, etc., can be used.

6. **Memory Functions (also in `<string.h>`)**:
    - Sometimes, when working with strings or raw memory regions, the following functions can be helpful:
      - `memcpy(dest, src, n)`: Copies `n` bytes from `src` to `dest`.
      - `memmove(dest, src, n)`: Similar to `memcpy`, but safe for overlapping memory areas.
      - `memcmp(ptr1, ptr2, n)`: Compares `n` bytes of two areas of memory.
      - `memset(ptr, value, n)`: Sets `n` bytes of memory starting at `ptr` to `value`.

7. **String and Pointers**:
    - Strings can also be represented using pointers. This is especially common when working with dynamic memory or string constants.
      ```c
      char *str_ptr = "Hello, pointer!";
      ```

note: since strings in C are just arrays of characters, it's essential to ensure proper memory allocation and avoid buffer overflows when working with strings. Always ensure that the array has space for the terminating null character. Functions like `strncpy` instead of `strcpy`, and `snprintf` instead of `sprintf`, can help avoid these issues by taking size parameters to ensure memory boundaries aren't breached.


### Understanding and Utilizing Arrays in C:

Arrays in C are fundamental data structures that allow you to store multiple items of the same type together. Understanding arrays is key to effective programming in C. Here's a deep dive into understanding and utilizing arrays in C:

### 1. Declaration & Initialization:

- **Static Array**:
  ```c
  int numbers[5];                      // Declares an array of 5 integers.
  char chars[6] = "Hello";             // 'Hello' + null character '\0'
  float values[] = {1.0, 2.5, 3.2};    // Size is determined by number of initializers.
  ```

- **Multi-dimensional Array**:
  ```c
  int matrix[2][3] = { 
      {1, 2, 3},
      {4, 5, 6}
  };
  ```

### 2. Accessing Array Elements:

- Using an index:
  ```c
  numbers[0] = 10;
  char firstChar = chars[0];
  ```

### 3. Size of Arrays:

- `sizeof` operator can determine the size of the array.
  ```c
  int size = sizeof(numbers) / sizeof(numbers[0]);  // Gives the number of elements in the array
  ```

### 4. Iterating Over Arrays:

- Commonly done using loops:
  ```c
  for(int i = 0; i < sizeof(numbers)/sizeof(numbers[0]); i++) {
      printf("%d\n", numbers[i]);
  }
  ```

### 5. Passing Arrays to Functions:

- Arrays decay to pointers when passed to functions. Hence, size information is lost.
  ```c
  void printArray(int arr[], int size) {
      for(int i = 0; i < size; i++) {
          printf("%d ", arr[i]);
      }
  }
  ```

### 6. Arrays and Pointers:

- The name of an array is a pointer to its first element.
  ```c
  int *p = numbers; // p points to the first element of the numbers array.
  ```

- This allows array-style indexing with pointers:
  ```c
  printf("%d", *(p+1)); // This will print the second element of the numbers array.
  ```

### 7. Character Arrays:

- Strings in C are character arrays terminated by a null character (`'\0'`).
  ```c
  char name[] = "John";
  ```


### 8. Multi-dimensional Arrays:

- Essentially "arrays of arrays".
  ```c
  int table[3][4];  // Represents a table with 3 rows and 4 columns.
  ```

- Iteration:
  ```c
  for(int i = 0; i < 3; i++) {
      for(int j = 0; j < 4; j++) {
          printf("%d ", table[i][j]);
      }
      printf("\n");
  }
  ```

### 9. Dynamic Arrays:

- C doesn't support dynamic arrays directly. However, using pointers and memory functions, dynamic allocation is possible.
  ```c
  int *dynamicArray;
  int size = 5;
  dynamicArray = (int*)malloc(size * sizeof(int));

  // Remember to free the memory after use
  free(dynamicArray);
  ```

### Best Practices & Notes:

1. **Bounds Checking**: C does not perform automatic bounds checking. Accessing outside the bounds of an array can lead to undefined behavior.

2. **Memory**: Arrays declared within functions (not as static or global) reside on the stack. Large arrays might exhaust stack space. In such cases, consider dynamic allocation using `malloc()` which allocates on the heap.

3. **Initialization**: Always initialize arrays if you're planning to access them before setting a value. Uninitialized arrays will have garbage values.

Arrays, combined with loops and functions, form the backbone of many algorithms and data processing in C. Proper understanding and careful usage are crucial to write efficient and error-free programs.


## Wednesday:

Continue with the course as planned.

Continue working on the C project "word searcher":
- Read a file.
- For each word in the file, keep track of how many times each word occurs.
- Provide an option to sort and display the words based on their occurrence count (increasing or decreasing order).
- Write a report showing the top 10 words and their occurrence count.
- Implement the ability to search for how many times a specific word occurs.

Remember to manage memory properly, handle file operations securely, and implement efficient algorithms for counting and sorting words.

## Thursday:

Continue with the course.
