
The next report is the call graph, which shows the breakdown of time by individual functions and how the functions were called:

```
index % time self children called name
<spontaneous>
[1] 100.0 0.00 33.99 main [1]
22.78 11.19 50000/50000 function2 [2]
0.02 0.00 100/50100 function1 [3]
------------------------------------------------------------
22.78 11.19 50000/50000 main [1]
[2] 99.9 22.78 11.19 50000 function2 [2]
11.19 0.00 50000/50100 function1 [3]
------------------------------------------------------------
0.02 0.00 100/50100 main [1]
11.19 0.00 50000/50100 function2 [2]
[3] 33.0 11.21 0.00 50100 function1 [3]
```

Each section of the call graph shows the function analyzed (the one on the line with the index number), the functions that called it, and its child functions. This output is used to see the flow of time throughout the program.

## Writing C Programs

With a full C programming environment pre-installed on your Ubuntu system, you're ready to start coding C programs. This section walks through the basics of programming in C.

## C Program Format

Possibly one of the most confusing parts of C programming is the precise format used in creating C programs. The C language is picky about how it handles things. There are generally three sections in a C program:

- Headers section
- Declaration section
- Code section

The content of each of these sections is described in the following sections.

## Header Section

In the headers section, variables and functions used in external libraries are declared in header files. The files are separate from the main program and must be declared so that the compiler knows where to get them. Standard library header files are specified in the format:

```
#include <library>
```

where library is the header file name (usually with a .h extension). If your code uses any of the standard input and output functions, you'll need to define the stdio.h header file in your C program:

```
#include <stdio.h>
```

Alternatively, if you create your own functions, they should have their own header files, which may be located in the same folder as the main program code. The format to declare that file is

```
#include "local.h"
```

where local.h is the name of the local function header file.

## Declaration Section

The declaration section defines all of the variables and functions used in the program. In the C language, you must declare the data type of a variable, and the variable can hold only that type of data for the entire program. C supports many types of data. Table 27-9 lists the basic data types you can use in your programs.

| Table 27-9: The C Language Basic Data Types |
| Parameter | Description |
| int | Integer value (32 bits) |
| float | Floating-point, single-precision value (32 bits) |
| double | Floating-point, double-precision value (64 bits) |
| char | A single character value (8 bits) |
| void | No data |

Besides the data types there are also modifiers, which define the storage allocated for a specific data type. There isn't a set standard on the amount of storage used when modifiers are defined, but generally they're

- Short: Half of the normal size, so a short int value is 16 bits
- Long: Double the normal size, so a long int value is 64 bits
- Signed: Contains negative and positive values; a signed int value can have a value between -32,768 and +32,767
- Unsigned: Contains only positive values; a signed int value can have a value between 0 and 65,535

> With the popularity of 64-bit computing platforms, the base size of data types is changing. While some data types double in size (such as int and float) others stay the same (such as char).

The declaration section declares a data type, a variable name, and an optional default variable value:

```
int counter;
float price = 0.00;
char data;
```

Each variable declaration remains in effect for the entire program. In the C language, once you declare the data type of a variable you can't store data from other data types in that variable.

## Code Section

The C program itself is defined as a code block enclosed in braces. The code block must have a name and a declared data type. There can be any number of code blocks defined in a single C program file. Each code block must have a unique name assigned to it.

The starting code block in every C program is called main. That's how the compiler knows where to start the program. You must also declare a return data type for each code block. This is the type of data that's expected to be returned when the code block completes.

The main code block must return an integer data type to the operating system. The operating system will then pass the return value to the shell so that you can tell whether your program terminated properly.

The general format for the code block is

```
int main()
{
local variables

code
}
```

Inside the code block you can also declare additional variables. These are called local variables, and they are available for use only inside the code block. Any variables declared in the declaration section are considered global variables and can be used in any of the code blocks in the program.

> Be careful when creating C programs on your Ubuntu system. The program file must be a plain text file, without any formatting code. Most word-processing programs (such as the OpenOffice.org Writer program) add binary formatting codes to the text file, which will confuse the C compiler. It's best to use the Ubuntu gedit text editor to create your C program files, and make sure that you save them with the .c file extension.
