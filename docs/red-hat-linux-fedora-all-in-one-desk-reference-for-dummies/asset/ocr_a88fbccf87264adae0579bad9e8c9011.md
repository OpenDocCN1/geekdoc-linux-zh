mistakes you might make when calling a function, such as passing the wrong number of arguments (when the function takes a fixed number of arguments) or passing a wrong type of argument to a function.

# The void type

What do you do when a function doesn't return anything nor accept any parameters? To handle these cases, C provides the void type, which is useful for declaring functions that return nothing and for describing pointers that can point to any type of data. For example, you can use the void return type to declare a function such as exit that does not return anything:

```
void exit(int status);
```

On the other hand, if a function doesn't accept any formal parameters, its list of arguments is represented by a void:

```
FILE *tmpfile(void);
```

The void pointer is useful for functions that work with blocks of memory. For example, when you request a certain number of bytes from the memory allocation routine malloc, you can use these locations to store any data that fits the space. In this case, the address of the first location of the allocated block of memory is returned as a void pointer. Thus, the prototype of malloc is written as follows:

```
void *malloc(size_t numbytes);
```

# Functions with a variable number of arguments

If a function accepts a variable number of arguments, you can indicate this by using an ellipsis (...) in place of the argument list; however, you must provide at least one argument before the ellipsis. A good example of such functions is the printf family of functions defined in the header file stdio.h. The prototypes of these functions are as follows:

```
int fprintf(FILE *stream, const char *format, ...);
int printf(const char *format, ...);
int sprintf(char *buffer, const char *format, ...);
```

# The C Library

The ANSI and ISO standards for C define all aspects of C — the language, the preprocessor, and the library. The prototypes of the functions in the library, as well as all necessary data structures and preprocessor constants, are defined in a set of standard header files. Table 2-4 lists the standard header files, including a summary of their contents.