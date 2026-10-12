this returned pointer inside a pointer variable in your program, it can be converted into a pointer of the appropriate type using the type cast operator.

The m        function works similarly, except that it only takes a single argument—the total number of bytes of storage to allocate—and also doesn’t automatically set the storage area to 0.

The dynamic memory allocation functions are declared in the standard header file <        , which should be included in your program whenever you want to use these routines.

# ## The sizeof Operator

To determine the size of data elements to be reserved by c        or m        in a machine-independent way, the C `sizeof` operator should be used. The `sizeof` operator returns the size of the specified item in bytes. The argument to the `sizeof` operator can be a variable, an array name, the name of a basic data type, the name of a derived data type, or an expression. For example, writing `sizeof(int)`

```
```
sizeof(int)
```
```

gives the number of bytes needed to store an integer. On a Pentium 4 machine, this has the value 4 because an integer occupies 32 bits on that machine. If x is defined to be an array of 100 integers, the expression `sizeof(x)`

```
```
sizeof(x)
```
```

gives the amount of storage required for the 100 integers of x (or the value 400 on a Pentium 4). The expression `sizeof(struct d)`

```
```
sizeof(struct d)
```
```

has as its value the amount of storage required to store one d        structure. Finally, if d is defined as an array of `sizeof(int)` elements, the expression `Click here to view code image`

`Click here to view code image` `sizeof(d)`

gives the number of elements contained in d    (d        must be a previously defined array, and not a formal parameter or externally referenced array). The expression `Click here to view code image`

```
```
sizeof(d) / sizeof(int)
```
```

also produces the same result. The macro `Click here to view code image` `#define sizeof`

```
```
#define sizeof
```
```

simply generalizes this technique. It enables you to write code like `Click here to view code image`

```
```
i
```
```

and `Click here to view code image`

```
```
sizeof(d) / sizeof(int)
```
```

You should remember that `sizeof`        is actually an operator, and not a function, even though it looks like a function. This operator is evaluated at compile time and not at runtime, unless a variable-length