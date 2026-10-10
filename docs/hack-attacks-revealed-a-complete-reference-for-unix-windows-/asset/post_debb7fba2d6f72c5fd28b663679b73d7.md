
## Structure of C

C programs are written in a structured manner. A collection of code blocks are created that call each other to comprise the complete program. As a structured language, C provides various looping and testing commands, such as:

- do-while, for, while, if

A C code block is contained within a pair of curly braces (`{ }`), and may be a complete procedure called *a function*, or a subset of code within a function. For example, the following is a code block:

```
if (x < 10) 
{    
    a = 1;  
    b = 0;  
}
```

The statements within the curly braces are executed only upon satisfaction of the condition that x < 10.

This next example is a complete function code block, containing a subcode block as a do-while loop:

```
int GET_X() 
{ 
    int x;  
    do 
    { 
        printf ("\nEnter a number between 0 and 10 "); 
        scanf ("%d", &x);  
    } while (x < 0 || x > 10);  
    return (x);  
}
```

Notice that every statement line is terminated in a semicolon, unless that statement marks the start of a code block, in which case it is followed by a curly brace. C is a case-sensitive, but free-flowing language; spaces between commands are ignored, therefore the semicolon delimiter is required to mark the end of the command line. As a result of its free-flow structure, the following commands are recognized as the same by the C compiler:

```
x = 0; 
x      = 0; 
x=0;
```

The general form of a C program is as follows:

- Compiler preprocessor statements
- Global data declarations
- Return-type main (parameter list)

```
{ 
    statements
    return-type f1(parameter list)
    {
        statements
    }
    return-type f2(parameter list)
    {
        statements
    }
    .
    .
    return-type fn(parameter list)
    {
        statements
    }
}
```

### Comments

As with most other languages, C allows comments to be included in the program. A comment line is enclosed within `/*` and `*/`:

```
/* This is a legitimate C comment line */
```

### Libraries

C programs are compiled and combined with library functions provided with the C compiler. These libraries are composed of standard functions, the functionalities of which are defined in the ANSI standard of the C language; they are provided by the individual C compiler manufacturers to be machine-dependent. Thus, the standard library function printf() provides the same facilities on a DEC VAX as on an IBM PC, although the actual machine language code in the library is quite different for each. The C programmer, however, does not need to know about the internals of the libraries, only that each library function will behave in the same way on any computer.

### C Compilation

Before we reference C functions, commands, sequences, and advanced coding, we'll take a look at actual program compilation steps. Compiling C programs are relatively easy, but they are distinctive to specific compilers. Menu-driven compilers, for example, allow you to compile, build, and execute programs in one keystroke. For all practical purposes, we'll examine these processes from a terminal console.

From any editor, enter in the following snippet and save the file as *example.c*:

```
/*
    simple pop-up text message
*/
#include<stdio.h>
void main()
{
    printf( "Wassup!!!\n" );
}
```

At this point, we need to compile our code into a program file, before the snippet can be run, or executed. At a console prompt, in the same directory as our newly created *example.c*, we enter the following compilation command:

```
cc example.c
```

Note that compilation command syntax varies from compiler to compiler. Our example is based on the C standard. Currently, common syntax is typically derived from the GNU C compiler, and would be executed as follows:

```
gcc example.c
```

After successful completion, our sample snippet has been compiled into a system program file and awaits execution. The output, obviously deduced from the simple code, produces the following result:

```
Wassup!!!
Press any key to continue
```

That's all there is to it! C snippet compilation is relatively easy; however, be aware of the results of destructive penetration programs. Of course, the exploit coding found throughout this book and available on the accompanying CD is much more complicated, but you get the idea.

### Data Types

There are four basic types of data in the C language: character, integer, floating point, and valueless, which are referred to by the C keywords: *char*, *int*, *float*, and *void*, respectively. Basic data types may be added with the following type modifiers: *signed*, *unsigned*, *long*, and *short*, to produce further data types. By default, data types are assumed signed; therefore, the signed modifier is rarely used, unless to override a compiler switch defaulting a data type to unsigned. The size of each data type varies from one hardware platform to another, but the narrowest range of values that can be held is described in the ANSI standard, given in Table 7.1.

In practice, this means that the data type *char* is particularly suitable for storing flag type variables, such as status codes, which have a limited range of values. The *int* data type can be used, but if the range of values does not exceed 127 (or 255 for an unsigned char), then each declared variable would be wasting storage space.

Which real number data type to use—*float*, *double*, or *long double*—is a tricky question. When numeric accuracy is required, for example in an accounting application, instinct would be to use the long double, but this requires at least 10 bytes of storage space for each variable. Real numbers are not as precise as integers, so perhaps integer data types should be used instead, and work around the problem. The data type *float* is worse, since its six-digit precision is too inaccurate to be relied upon. Generally, you should use integer data types wherever possible, but if real numbers are required, then use a *double*.

**Table 7.1 C Data Type Sizes and Ranges**

| TYPE | SIZE | RANGE |
| :--- | :--- | :--- |
| Char | 8 | -127 to 127 |
| unsigned char | 8 | 0 to 255 |
| Int | 16 | -32767 to 32767 |
| unsigned int | 16 | 0 to 65535 |
| long int | 32 | -2147483647 to 2147483647 |
| unsigned long int | 32 | 0 to 4294967295 |
| Float | 32 | 6-digit precision |
| Double | 64 | 10-digit precision |
| long double | 80 | 10-digit precision |

### Declaring a Variable

All variables in a C program must be declared before they can be used. The general form of a variable definition is:

```
type name;
```

So, for example, to declare a variable x, of data type int so that it may store a value in the range -32767 to 32767, you use the statement:

```
int x;
```

Character strings may also be declared as arrays of characters:

```
char name[number_of_elements];
```

To declare a string called *name* that is 30 characters in length, you would use the following declaration:

```
char name[30];
```

Arrays of other data types may be declared in one, two, or more dimensions as well. For example, to declare a two-dimensional array of integers, you would use:

```
int x[10][10];
```

The elements of this array are accessed as:

```
x[0][0]
x[0][1]
x[n][n]
```

There are three levels of access to variables; local, module, and global. A variable declared within a code block is known only to the statements within that code block. A variable declared outside any function code blocks, but prefixed with the storage modifier “static,” is known only to the statements within that source module. A variable declared outside any functions, and not prefixed with the static storage type modifier, may be accessed by any statement within any source module of the program. For example:

```
int error;
static int a;

main()
{
    int x;
    int y;
}

func a()
{
    /* Test variable 'a' for equality with 0 */
    if (a == 0)
    {
        int b;
        for (b = 0; b < 20; b++)
            printf("\nHello World");
    }
}
```

In this example the variable *error* is accessible by all source code modules compiled together to form the finished program. The variable *a* is accessible by statements in both functions main() and func a(), but is invisible to any other source module. Variables *x* and *y* are accessible only by statements within function main(). Finally, the variable *b* is accessible only by statements within the code block following the *if* statement.

If a second source module wanted to access the variable *error*, it would need to declare *error* as an *extern* global variable, such as:

```
extern int error;
```

```
func b()
{

}
```

C will readily allow you to assign different data types to each other. For example, you may declare a variable to be of type *char*, in which case a single byte of data will be allocated to store the variable. You can attempt to allocate larger values to this variable:

```
main()
{
    x = 5000;
}
```

In this example, the variable *x* can only store a value between -127 and 128, so the figure 5000 will *not* be assigned to the variable *x*. Rather the value 136 will be assigned.

Often, you may wish to assign different data types to each other; and to prevent the compiler from warning of a possible error, you can use a *cast statement* to tell the compiler that you know what you're doing. A cast statement is a data type in parentheses preceding a variable or expression:
