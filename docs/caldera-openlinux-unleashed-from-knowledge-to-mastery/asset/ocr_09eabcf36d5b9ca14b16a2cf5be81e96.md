+   - **int**  A signed integer, which is the “natural” size for the processor. Even though **int** is 32 bits under most versions of Linux, you should not count on this. ANSI specifies that **int** must be able to hold values from –32767 to 32767, and that’s all you can count on.
+   
+   - **short int**  A signed integer that may be smaller than int. A **short int** is 16 bits long under most versions of Linux, but do not count on this. An implementation may very well make **short int** and **int** the same.
+   
+   - **long int**  A signed integer that may be larger than int. ANSI specifies that **long int** must be able to hold values from –2147483647 to 2147483647. On many Linux architectures, a **long int** is the same size as an **int**. This is not true for 64-bit architectures.
+   
+   - **unsigned int**  An unsigned integer that is the same size as an int. There are analogous unsigned short and unsigned long types. An unsigned type cannot represent negative values but can represent positive numbers about twice as large as the largest value that can be represented by the corresponding signed type.
+   
+   - **char**  A type that can represent a single character. An implementation may treat char as signed or unsigned; the standard does not specify which. If you really need one or the other, specify whether it is to be unsigned or signed.
+   
+   - **float**  A type that represents a floating-point number.
+   
+   - **double**  A type that represents a floating-point number, possibly with higher precision than **float**.
+   
+   - **void**  A type that represents nothing. You cannot directly declare a variable of type **void**, but you can use it as the return type of a function that doesn’t return anything useful or as the type of a pointer. (We discuss this type in more detail later.)

# ## Declaring Variables

To create a variable of a specified type, you declare the variable. In this simplest case, this is statement consisting of the type and the variable name. Consider this example:

```
```c
int a;
double c, d;
unsigned long foobar;
```
```

This declares four variables: a of type **int**, c and d of type **double**, and foobar of type **unsigned long**.