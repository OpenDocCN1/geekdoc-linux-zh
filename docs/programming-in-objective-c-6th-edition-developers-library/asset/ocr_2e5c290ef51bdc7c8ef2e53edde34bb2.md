Before the type declaration, an optional storage class might also be specified, as summarized in **Section 6.2**. If a storage class is specified, and the type of the variable is **i** , then **i** can be omitted. For example,

```
```
  
        declares **c** to be a **s** variable.
```

Note that the **s** modifier can also be placed in front of the **s** , **i** , **l** , and **1** types. Because these types are signed by default anyway, this has no effect.

**\_** and **\-** data types enable complex and imaginary numbers to be declared and manipulated, with functions in the library for supporting arithmetic on these types. Normally, you should include the file **\_** in your program, which defines macros and declares functions for working with complex and imaginary numbers. For example, a **d** variable **c** can be declared and initialized to the value **5** with a statement such as:
```

![](bbox=[0.02, 0.3, 0.25, 0.31])

```
```
  
d
```

Library routines such as **c** and **c** can then be used to extract the real and imaginary part of **c** , respectively.

An implementation is not required to support types **\_** and **\_** , or it can optionally support one but not the other.

The header file **\_** can be included in a program to make working with Boolean variables easier. In that file, the macros **b** , **t** , and **f** are defined, enabling you to write statements such as:
```

```
```
    b
```

```

# # 4.3 Derived Data Types

A derived data type is one that is built up from one or more of the basic data types. Derived data types are arrays, structures, unions, and pointers. A function that returns a value of a specified type is also considered a derived data type. Each of these, with the exception of functions, is summarized in the following sections. Functions are separately covered in **Section 7.0.**

# ## 4.3.1 Arrays

### Single-Dimensional Arrays

Arrays can be defined to contain any basic data type or any derived data type. Arrays of functions are not permitted (although arrays of function pointers are).

The declaration of an array has the following basic format:

![](bbox=[0.02, 0.8, 0.25, 0.82])

```
```
  
t          name[n]
```

The expression *n* determines the number of elements in the array *name* and can be omitted provided a list of initial values is specified. In such a case, the size of the array is determined based on the number of initial values listed or on the largest index element referenced if *designated initializers* are used.
```