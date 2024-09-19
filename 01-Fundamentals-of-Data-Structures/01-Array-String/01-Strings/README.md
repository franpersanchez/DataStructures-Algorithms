# **STRINGS**

## **_JAVA_**

### **Character Indexing**

Each character `c` within a string `s` can be referenced by using an index, which is equal to the number of characters that come before `c` in `s`. Java’s `String` class supports:

- **`length()`**: Returns the length of the string instance.
- **`charAt(k)`**: Returns the character at index `k`.

Example:
```java
String s = "hello";
int length = s.length();    // Returns 5
char c = s.charAt(1);      // Returns 'e'
```
### **Concatenation**
Concatenation combines two strings into a new string, denoted P+Q, which consists of all the characters of P followed by all the characters of Q. In Java, the “+” operator performs concatenation when acting on two strings:

Example:

```java
String P = "hello";
String Q = " world";
String result = P + Q;  // Result: "hello world"`
```

### **The StringBuilder Class**
Java’s **String** class is **immutable**; once an instance is created and initialized, its value cannot be changed. However, Java provides the StringBuilder class for more efficient string manipulation. It is mutable and allows modification of its content.

Key methods of StringBuilder:

- setCharAt(k, c): Change the character at index k to c.
- insert(k, s): Insert a copy of string s starting at index k, shifting existing characters to the right.
- append(s): Append string s to the end of the sequence.
- reverse(): Reverse the current sequence.
- toString(): Convert StringBuilder to a traditional String.

Example:

```java
StringBuilder sb = new StringBuilder("hello");
sb.setCharAt(0, 'H');
sb.append(" world");
String result = sb.toString();  // Result: "Hello world"
```
---
---
## **_C_**

### **Character Indexing**
In C, strings are arrays of characters, and each character in the string occupies 1 byte (8 bits) of memory. When you declare a string, memory is allocated to store each character in the array, plus one extra byte for the null terminator ('\0'), which signifies the end of the string.

Example:

```c
#include <stdio.h>

int main() {
    char s[] = "hello";
    int length = 0;
    while (s[length] != '\0') {
        length++;
    }
    char c = s[1];  // Returns 'e'
    printf("Length: %d, Character: %c\n", length, c);
    return 0;
}
```
If you need a string with dynamic memory allocation (e.g., for strings of unknown size), you use malloc() or calloc() to allocate the memory dynamically. For example:

```c
char *s = (char *)malloc(6 * sizeof(char));  // Allocates 6 bytes for "hello\0"
```

### **Concatenation**

In C, concatenation is performed using the **strcat**() function from the string.h library. **Ensure the destination buffer is large enough to hold the resulting string.**

Example:

```c
#include <stdio.h>
#include <string.h>

int main() {
    char dest[100] = "hello";
    char src[] = " world";
    strcat(dest, src);
    printf("Result: %s\n", dest);  // Output: hello world
    return 0;
}

```
String Manipulation
In C, strings are managed using arrays of characters and various functions from the string.h library. C does not have a built-in mutable string class like Java’s StringBuilder.

Common functions include:

* strcpy(dest, src): Copy string src to dest.
* strlen(s): Returns the length of the string s.
* strcmp(s1, s2): Compare two strings s1 and s2.

Example:
```c
#include <stdio.h>
#include <string.h>

int main() {
    char s1[20] = "hello";
    char s2[] = " world";
    strcat(s1, s2);        // Concatenate s2 to s1
    printf("Concatenated: %s\n", s1);  // Output: hello world

    char s3[20];
    strcpy(s3, s1);       // Copy s1 to s3
    printf("Copied: %s\n", s3);  // Output: hello world

    int len = strlen(s3);  // Get length of s3
    printf("Length: %d\n", len);  // Output: 11

    return 0;
}
```
---
### What's the difference between char *s = "hello"; y char s[] = "hello"; in **C**?

The two declarations char *s = "hello"; and char s[] = "hello"; are both used to create strings in C, but they have significant differences in how the memory is managed and how the string can be used. Let's break down the differences:

1. char *s = "hello"; – Pointer to a String Literal
Type: 
This declares s as a pointer to a string literal, where "hello" is stored in a read-only section of memory (commonly in the text segment).
Memory: The string "hello" is stored in a read-only section of memory, and s holds the address of the first character of that string. The characters cannot be modified.
Modifiability: You cannot modify the string through s. Any attempt to modify it results in undefined behavior or a segmentation fault because string literals are typically stored in read-only memory.
Example:

```c
char *s = "hello";
// s points to a read-only string "hello"
// You cannot change s[0] = 'H'; // This will cause a runtime error
```
**Use case:** When you don’t need to modify the string and want to save memory by using a pointer to a constant string.


2. char s[] = "hello"; – Array of Characters
Type: This declares s as a character array, where the content "hello" is copied into the array at the time of initialization.
Memory: The array s is allocated on the stack (or heap, depending on where it is declared) and contains a writable copy of the string "hello". The size of the array is automatically determined by the size of the string literal (including the null terminator).
Modifiability: You can modify the contents of the array. Each character in s can be changed because the array holds its own copy of the string.

Example:

```
c
char s[] = "hello";
// s is an array with a copy of "hello"
s[0] = 'H'; // This is allowed, and s now holds "Hello"
```
Use case: When you need to modify the string or store a string in writable memory.

### Key Differences
Feature | char *s = "hello"; | char s[] = "hello";
--------|--------------------|--------------------
Memory Location | String literal in read-only memory (typically text segment) | Array stored in stack memory (local variable) or heap (global/static)
Modifiability | Cannot modify the string | Can modify the array's contents
Size | s is a pointer (size of a pointer) | Array size is determined by string length (including \0)
Null-Terminated | Yes (string literal) | Yes (as it’s an array of characters initialized with "hello")
Example Modification | s[0] = 'H'; // Causes error | s[0] = 'H'; // Modifies string
Use Case | String literal (read-only) | Writable string (modifiable)


### Memory Allocation
char *s = "hello";: The pointer s points to the first character of the string literal "hello". This string is placed in a read-only section of memory (usually the text segment), and trying to modify it will cause a runtime error.

```lua
Copiar código
Memory Layout:
+---+---+---+---+---+----+
| h | e | l | l | o | \0 |
+---+---+---+---+---+----+
   ^
   |
   s (points to read-only memory)

```
char s[] = "hello";: The string "hello" is copied into a local array s that resides in writable memory. The array is automatically sized to hold the string and the null terminator (\0), so its size is 6 characters.

```diff
Memory Layout:
+---+---+---+---+---+----+
| h | e | l | l | o | \0 |
+---+---+---+---+---+----+
s[0]
```
### Which One to Use?
* Use char *s = "hello"; when you don't need to modify the string and want to conserve memory by pointing to a string literal.
* Use char s[] = "hello"; when you need to modify the string or ensure it’s stored in writable memory.