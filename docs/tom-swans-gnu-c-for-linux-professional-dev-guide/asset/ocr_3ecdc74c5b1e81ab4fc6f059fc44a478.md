There is no memory leak here because the function preserves the address of the allocated memory by returning it as the function result. Notice the function’s type is `double *` (double pointer). Managing the allocated memory is now the responsibility of the function’s caller. Elsewhere in the program, a statement can declare a double pointer and call `f()` like this:

```c
double *dynamic_dp = f();
```

The function `f()` allocates space for a double value, assigns 3.14159 to that object, and returns the pointer, which the program assigns to `dynamic_dp`. This plugs the leak, but the memory must still be deleted at some point, using the following statement:

```c
delete dynamic_dp;
```

# MEMORY MANAGEMENT WITH malloc() AND free()

Many existing C programs use standard library functions to allocate and free memory, and it’s good to know how to use the techniques if only so that you can read and understand those programs’ source files. In new code, use the C++ `new` and `delete` operators.

To use C memory management functions, include the `stdlib.h` header file using the directive

```c
#include <stdlib.h>
```

This makes the following four functions available to your program:

```
void *malloc(size_t size);
void *calloc(size_t n, size_t size);
void *realloc(void *ptr, size_t size);
void free(void *ptr);
```

Several other memory allocation functions are in the standard C library, but those four are the most commonly used. The first three functions allocate memory. The `free()` function deletes previously allocated memory. Memory allocators return type `void *`, literally a pointer with no type, that can be assigned to any pointer variable. If enough memory is not available, memory allocation functions return `NULL`. The `free()` function returns no value.

> I explain here only how to use `malloc()`. For online documentation on using `calloc()`, `realloc()`, and other standard C library memory functions, use the command `man malloc`. For the full ball of wax on C memory management functions, use the command `info libc` and step to the node *Memory Management*. Depending on your Linux version, this might be named *Memory Allocation*.

Calling `malloc()` reserves size bytes of memory. The following statements declare a double pointer and then call `malloc()` to allocate space for one double value:

```
double *dp;
dp = (double *) malloc( sizeof(double) );
```

Obviously, using the C++ `new` operator is simpler. In plain C, the type cast expression isn’t needed, and you will find numerous statements such as the following in C source files:

```
dp = malloc( sizeof(double) );
```