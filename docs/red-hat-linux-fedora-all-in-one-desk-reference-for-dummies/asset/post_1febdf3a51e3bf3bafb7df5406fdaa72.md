
![](img/a7eec43a54473e95dc5ea333fecf1bd7_765_0.png)

To create an executable program, you must compile and link the source files. The exact steps for building programs from C source files depend on the compiler and the operating system. For example, in Red Hat Linux, you can compile and link the files shown in Figure 2-1 with the following command:

```
gcc -o shapetest shapetest.c shapes.c
```

This command creates an executable file named shapetest. You can then run that file with the command

```
./shapetest
```

Here is the output the program displays:

```
Area of circle = 7853.981634
```

## Declaration versus definition

A declaration determines how the program interprets a symbol. A definition, on the other hand, actually creates a variable or a function. Definitions cause the compiler to set aside storage for data or code, but declarations do not. For example,

```
int x, y, z;
```

is a definition of three distinct integer variables, but

```
extern int x, y, z;
```

is a declaration, indicating that the three integer variables are defined in another source file.

Within each source file, the components of the program are laid out in a standard manner. As the files illustrated in Figure 2-1 show, the typical components of a C source file follow a certain order if you were to scroll down through them on-screen:

- 1. The file starts with some comments that describe the purpose of the module and provide some other pertinent information, such as the name of the author and revision dates. In C, comments start with /* and end with */.
- 2. Commands for the preprocessor, known as preprocessor directives, follow the comments. The first few directives typically are for including header files and defining constants.
- 3. Declarations of variables and functions that are visible throughout the file come next. In other words, the names of these variables and functions may be used in any of the functions in this file. Here, you also define variables needed within the file.
- 4. The rest of the file includes definitions of functions. Inside a function's body, you can define variables that are local to the function and that exist only while the function's code is being executed.

## Preprocessor Directives

Preprocessing refers to the first step in translating or compiling a C file into machine instructions. The preprocessor processes the source file and acts on certain commands (called preprocessor directives) embedded in the program. These directives begin with the hash mark (#) followed by a keyword. Usually the compiler automatically invokes the preprocessor before beginning compilation, but most compilers give you the option of invoking the preprocessor alone. You can utilize three major capabilities of the preprocessor to make your programs modular, more readable, and easier to customize:

- You can use the `#include` directive to insert the contents of a file into your program. With this, you can place common declarations in one location and use them in all source files through file inclusion. The result is a reduced risk of mismatches between declarations of variables and functions in separate program modules.
- Through the `#define` directive, you can define macros that enable you to replace one string with another. You can use the `#define` directive to give meaningful names to numeric constants, thus improving the readability of your source files.
- With directives such as `#if`, `#ifdef`, `#else`, and `#endif`, you can compile only selected portions of your program. You can use this feature to write source files with code for two or more systems, but compile only those parts that apply to the computer system on which you compile the program. With this strategy you can maintain multiple versions of a program using a single set of source files.

## Including files

You can write modular programs by exploiting the `#include` directive. This is possible because the C preprocessor enables you to keep commonly used declarations in a single file that you can insert in other source files as needed. ANSI C supports three forms of the `#include` directive. As a C programmer, you should be familiar with the first two forms:

```
#include <stdio.h>
#include "shapes.h"
```

You use the first form of `#include` to read the contents of a file — in this case, the standard C header file `stdio.h` from the default location where all the header files reside. Put the filename within double quotes when the file (for example, `shapes.h`) is in the current directory. The exact conventions for locating the included files depend on the compiler.

## Defining macros

A `macro` is essentially a short name for a reusable block of C code. The code can be as simple as a numerical constant or as complicated as many lines of detailed C code. The idea is that after you define a macro, you can use that macro wherever you want to use that code in your program. When the source file is preprocessed, every occurrence of a macro's name is replaced with its definition.

A common use of macros is to define a symbolic name for a numerical constant and then use the symbol instead of the numbers in your program. This improves the readability of the source code; with a descriptive name, you

aren't left guessing why a particular number is being used in the program. You can define such macros in a straightforward manner using the #define directive. Here are some examples:

```
#define PI 3.14159
#define GRAV_ACC 9.80665
#define BUFSIZE 512
```

After these symbols are defined, you can use PI, GRAV_ACC, and BUFSIZE instead of these numerical constants throughout the source file.

Macros, however, can do much more than simply replace a symbol for a constant or some block of code. A macro can accept a parameter and replace each occurrence of that parameter with the provided value when the macro is used in a program. Thus, the code that results from the expansion of a macro can change depending on the parameter you use when running the macro. For example, here is a macro that accepts a parameter and expands to an expression designed to calculate the square of the parameter:

```
#define square(x) ((x)*(x))
```

If you use square(z) in your program, it becomes ((z)*(z)) after the source file is preprocessed. In effect, this macro is equivalent to a function that computes the square of its arguments — except you don't call a function. Instead, the expression generated by the macro is placed directly in the source file.

## Conditional directives

You can use the conditional directives, such as #if, #ifdef, #ifndef, #else, #elif, and #endif, to control which parts of a source file are compiled and under what conditions. With this feature, you maintain a single set of source files that can be selectively compiled with different compilers and in different environments. (Another common use is to insert printf statements for debugging that are compiled only if a symbol named DEBUG is defined.) Conditional directives start with #if, #ifdef, or #ifndef — and may be followed by any number of #elif directives (or by none at all). Next comes an optional #else, followed by an #endif directive that marks the end of that conditional block. Here are some common ways of using conditional directives.

To include a header file only once, you can use the following:

```
#ifndef __PROJECT_H
#define __PROJECT_H
/* Declarations to be included once */
/* ... */
#endif
```

The following prints a diagnostic message during debugging (when the symbol DEBUG is defined):

```c
#ifdef DEBUG
printf("In read_file: bytes_read = %d\n", bytes_read);
#endif
```

The following example shows how you can include a different header file depending on the type of system for which the program is being compiled. To selectively include a header file, you can use the following:

```c
#if CPU_TYPE == I386
#include <i386sysdef.h>
#elif CPU_TYPE == M68K
#include <m68ksysdef.h>
#else
#error Unknown CPU type.
#endif
```

The #error directive is used to display error messages during preprocessing.

## Other directives

Several other preprocessor directives perform miscellaneous tasks. For example, you can use the #undef directive to remove the current definition of a symbol. The #pragma directive is another special purpose directive that you can use to convey information to the C compiler. You can use pragma to access the special features of a compiler — and those vary from one compiler to another.

C compilers provide several predefined macros (see Table 2-1). Of these, the macros __FILE__ and __LINE__ respectively refer to the current source filename and the current line number being processed. You can use the #line directive to change these. For example, to set __FILE__ to "file_io.c" and __LINE__ to 100, you say:

```c
#line 100 "file_io.c"
```

**Table 2-1 Predefined Macros in C**

| Macro | Definition |
|---|---|
| `__DATE__` | This is a string containing the date when you invoke the C compiler. It is of the form MMM DD YYYY (for example, Oct 26 2002). |
| `__FILE__` | This expands to a string containing the name of the source file. |
