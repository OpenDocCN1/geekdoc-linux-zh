
# Exploring the Software Development Tools in Fedora Core

- Variables are used to store different types of data. You can think of each variable as a placeholder for data — kind of a mailbox, with a name and room to store data. The content of that is its value.

- Expressions combine variables by using operators. An expression may add several variables; another may extract a part of a string.

- Statements perform some action, such as assigning a value to a variable or printing a string.

- Flow-control statements allow statements to execute in various orders, depending on the value of some expression. Typically, flow-control statements include for, `do-while`, `while`, and `if-else` statements.

- Functions (also called subroutines or routines) allow you to group statements and give them a name. This feature allows you to execute the same set of statements by invoking the function that represents those statements. Typically, a programming language provides many predefined functions to perform tasks such as opening (and reading) from a file.

# Exploring the Software Development Tools in Fedora Core

Fedora includes these traditional UNIX software-development tools:

- Text editors such as `vi` and `emacs` for editing the source code. (To find out more about `vi`, see Book II, Chapter 5.5.)

- A C compiler for compiling and linking programs written in C — the programming language of choice for writing UNIX applications (though nowadays programmers are turning to C++ and Java). Fedora Core includes the GNU C and C++ compilers. The GNU Compiler was known as GCC — which now stands for GNU Compiler Collection (see a description at `gcc.gnu.org`).

- The `make` utility for automating the software build process — the process of combining object modules into an executable or a library.

- A debugger for debugging programs. Fedora Core includes the debugger `gdb`.

- A version-control system to keep track of various revisions of a source file. Linux uses RCS (Revision Control System) and CVS (Current Versions System). Nowadays most open-source projects use CVS as their version-control system.

These tools install automatically if you select the Development Tools when you install Fedora Core from its companion DVD-ROM. In the next few sections, I briefly describe how to use these software-development tools to write applications for Fedora Core.

# Exploring the Software Development Tools in Fedora Core

## GNU C and C++ compilers

The most important software-development tool in Fedora Core is GCC — the GNU and C++ compiler. In fact, GCC can compile three languages: C, C++, and Objective-C (a language that adds object-oriented programming capabilities to C). You may use the gcc command to compile and link both C and C++ source files. The GCC compiler supports ANSI standard, making it easy to port any ANSI C program to Linux. In addition, if you've ever used a C compiler on UNIX systems, you're right at home.

## Using GCC

The gcc command to invoke GCC. By default, when you use the gcc command on a source file, GCC preprocesses, compiles, and links to create an executable file. However, you can use GCC options to stop this process at an intermediate stage. For example, you might invoke `gcc -c` option to generate an object file, but not perform the link step.

To compile and link C source files is very simple. Suppose you want to compile and link a simple program made up of two files. Use the following source for this task; it's stored in the file `area.c`, and it's the main program that computes the area of a circle whose radius is specified through the following command:

```c
#include <stdio.h>
#include <stdlib.h>

/* Function prototype */
double area_of_circle(double r);

int main(int argc, char **argv) {
    if (argc < 2) {
        printf("Usage: %s\n", argv[0]);
        exit(1);
    } else {
        double radius = atof(argv[1]);
        double area = area_of_circle(radius);
        printf("Area of circle with radius %f\n", radius, area);
    }
    return 0;
}
```

You need another file that actually computes the area of a circle. Here's the listing for `circle.c`, where I define a function that computes the area:

```c
#include <math.h>

#define SQUARE(x) ((x)*(x))

double area_of_circle(double r) {
    return 4.0 * M_PI * SQUARE(r);
}
```

For such a simple program, you could have placed everything in a single file, but this example shows you how to handle multiple files. To compile these two files and create an executable file named `area`, use this command:

```bash
gcc -o area area.c circle.c
```

This invocation of GCC uses the -o option to specify the name of the executable file. If you don't specify the name of the output file with the -o option, GCC saves the executable in a file named `a.out`.

If you have many source files to compile and link, you can compile files individually and generate object files (that have the .o extension). When you change a source file, you just need to compile that file into an object file. The following commands show how to separate the compile and link steps for the sample program:

```bash
gcc -c area.c
gcc -c circle.c
gcc -o area area.o circle.o
```

The first two commands run gcc with the -c option compiling the source files. The third links the object files into an executable area. In case you are curious, here's how you run the area program (to compute the area of a circle with a radius of 1):

```bash
./area 1
```

The program generates the following output:

Area of circle with radius 1.000000 = 12.56637

Incidentally, you have to add the prefix to the program's name (area) only if the current directory is not in the PATH environment variable. You do no harm in adding the prefix, even if your PATH contains the current directory.

![](img/d923b719dc0efd80851f36d8c6f571_742_0.png)

## Compiling C++ programs

GCC is a combined C and C++ compiler, so the gcc command can also compile C++ source files. GCC uses the file extension to determine whether a file is C or C++. C files have a lowercase .c extension, whereas C++ files end with .C or .cpp.

Although the gcc command can compile a C++ file, it does not automatically link with various class libraries that C++ programs typically require. That's why compiling and linking a C++ program using the g++ command is easy, which in turn runs gcc with appropriate options.

![](img/d923b719dc0efd80851f36d8c6f571_742_1.png)

Suppose you want to compile the following C++ program stored in a file named hello.C (using an uppercase C for C++ source files is customary):

```cpp
#include <iostream>
int main() {
    using namespace std;
    cout << "Hello from Fedora Core!" << endl;
}
```

To compile and link this program into an executable program named hello, use this command:

```bash
g++ -o hello hello.C
```

The command creates the hello executable, which you can run as follows:

```bash
./hello
```

The program displays the following output:

Hello from Fedora Core!

A host of GCC options controls various aspects of compiling C and C++ programs.

## Exploring GCC options

Here is the basic syntax of the gcc command:

```bash
gcc options filenames
```

Each option starts with a hyphen (-) and usually has a long name, as -funsigned-char or -finline-functions. Many commonly used options are short, however, such as -c, to compile all, and -g, to generate debugging information (needed to debug the program using the GNU debugger, gdb).

You can view a summary of all GCC options by typing the following command in a terminal:

```bash
man gcc
```

Then you can browse through the commonly used GCC options. Usually, you don't have to provide GCC options explicitly because the default settings are fine for most applications. Table 1-1 lists some of the GCC options you may use.

| Table 1-1 Commonly Used Options |
| :--- | :--- |
| **Option** | **Meaning** |
| -ansi | Support ANSI standard (ISO C89) syntax only. (This option disables some GNU C-specific features, such as the asm and typeof keywords.) |
| -c | Compile and generate object file. |
| -DMACRO | Define the macro with the string "1" as its value. |
| -DMACRO=DEFN | Define the macro as DEFN where DEFN is some text string. |
| -E | Run only the C preprocessor. |
| -fallow-single-precision | Perform all operations in single precision. |
| -fpcc-struct-return | Return all struct and union values in memory, rather than in registers. (Returning values this way is less efficient, but at least compatible with other compilers.) |
| -fPIC | Generate position-independent code (PIC) suitable for use in a shared library. |
| -freg-struct-return | When possible, return struct and union values in registers. |
| -g | Generate debugging information. (The GNU debugger can use this information.) |
