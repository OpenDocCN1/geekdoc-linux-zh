
as well as all necessary data structures and preprocessor constants, are defined in a set of standard header files. Table 2-4 lists the standard header files, including a summary of their contents.

## REMEMBER

If you're going to write applications in C, you have to become familiar with many of the standard libraries because that's where much of C's programming process lies. If you are writing graphical applications, you also must be familiar with other libraries such as the GIMP toolkit.

### Table 2-4 Standard Header Files in C

| **Header File** | **Purpose** |
| :--- | :--- |
| `<assert.h>` | Defines the `assert` macro. Used for program diagnostics. |
| `<ctype.h>` | Declares functions for classifying and converting characters. |
| `<errno.h>` | Defines macros for error conditions, `EDOM` and `ERANGE`, and the integer variable `errno` where library functions return an error code. |
| `<float.h>` | Defines a range of values that can be stored in floating-point types. |
| `<iso646.h>` | Defines a number of macros that are helpful when writing C programs in non-English languages that may use character combinations such as `&` and `--` for other purposes. |
| `<limits.h>` | Defines the limiting values of all integer data types. |
| `<locale.h>` | Declares the `lconv` structure and the functions necessary for customizing a C program to a particular locale. |
| `<math.h>` | Declares common mathematical functions and the `HUGE_VAL` macro. |
| `<setjmp.h>` | Defines the `setjmp` and `longjmp` functions that can transfer control from one function to another without relying on normal function calls and returns. Also defines the `jmp_buf` data type used by `setjmp` and `longjmp`. |
| `<signal.h>` | Defines symbols and routines necessary for handling exceptional conditions. |
| `<stdarg.h>` | Provides macros that provide access to the unnamed arguments in a function that accepts a varying number of arguments. |
| `<stddef.h>` | Defines the standard data types `ptrdiff_t`, `size_t`, `wchar_t`; the symbol `NULL`; and the macro `offsetof`. |
| `<stdio.h>` | Declares the functions and data types necessary for input and output operations. Defines macros such as `BUFSIZ`, `EOF`, `SEEK_CUR`, `SEEK_END`, and `SEEK_SET`. |
| `<stdlib.h>` | Declares many utility functions, such as the string conversion routines, random number generator, memory allocation routines, and process control routines (such as `abort`, `exit`, and `system`). |
| `<string.h>` | Declares the string manipulation routines such as `strcmp` and `strcpy`. |
| `<time.h>` | Defines data types and declares functions that manipulate time. Defines the types `clock_t` and `time_t` and the `tm` data structure. |
| `<wchar.h>` | Defines data types and declares functions for working with wide character data types (`wchar_t`). |
| `<wctype.h>` | Defines data types and declares functions for classifying and converting wide character data types (`wchar_t`). |

### Shared Libraries in Linux Applications

Most Linux programs use shared libraries. At a minimum, most C programs use the C shared library `libc.so.X`, wherein `X` is a version number. Using shared libraries is desirable because many executable programs can share the same shared library — you need only one copy of the shared library loaded into memory. Also, the *dynamic linking* (wherein a program loads code modules and links with them at runtime) is becoming increasingly popular because it enables an application to load blocks of code only when needed, thus reducing the memory requirement of the application.

When a program uses one or more shared libraries, you need the program’s executable file, as well as all the shared libraries, to run the program. In other words, your program doesn’t run if all shared libraries are not available on a system.

![](img/9f89727199836b0f871f1745838aa8b2_786_0.png)

If you sell an application that uses shared libraries, make sure all necessary shared libraries are distributed with your software.

The subject of shared libraries is of interest to Linux programmers because use of shared libraries reduces the size of executables. In this section I briefly describe how to create and use a shared library in a sample program.

#### Examining shared libraries that a program uses

Use the `ldd` utility to determine which shared libraries an executable program needs. Type the following `ldd` command to see the shared libraries used by a program (that was stored by GCC in the default file named `a.out`):

```
ldd a.out
```

Here is what `ldd` reports for a typical C program:

```text
libc.so.6 => /lib/tls/libc.so.6 (0x00b0a000)
/lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x00a0f1000)
```

A more complex program, such as the GIMP (an Adobe Photoshop-like program) uses many more shared libraries. To view its shared library needs, type the following command:

```bash
ldd /usr/bin/gimp
```

Here's the list displayed on my Fedora Core system:

```bash
libgimpwidgets-1.3.so.26 => /usr/lib/libgimpwidgets-1.3.so.26 (0x03783000)
libgimpcolor-1.3.so.26 => /usr/lib/libgimpcolor-1.3.so.26 (0x001ce000)
libgimpmodule-1.3.so.26 => /usr/lib/libgimpmodule-1.3.so.26 (0x001d8000)
libgimpbase-1.3.so.26 => /usr/lib/libgimpbase-1.3.so.26 (0x001a1000)
libgimptuumb-1.3.so.26 => /usr/lib/libgimptuumb-1.3.so.26 (0x00be000)
libgimpbase-1.3.so.26 => /usr/lib/libgimpbase-1.3.so.26 (0x000d7000)
libgtk-x11-2.0.so.0 => /usr/lib/libgtk-x11-2.0.so.0 (0x00448000)
libgdk-x11-2.0.so.0 => /usr/lib/libgdk-x11-2.0.so.0 (0x00762000)
libatk-1.0.so.0 => /usr/lib/libatk-1.0.so.0 (0x0073f000)
libgdk_pixbuf-2.0.so.0 => /usr/lib/libgdk_pixbuf-2.0.so.0 (0x003d5000)
libtcm.so.6 => /lib/tls/libtcm.so.6 (0x00c46000)
libXcursor.so.1 => /usr/lib/lib/libXcursor.so.1 (0x00191000)
libgpgpxo-1.0.so.0 => /usr/lib/libgpgpxo-1.0.so.0 (0x0075b000)
libgpgpxo-1.0.so.0 => /usr/lib/libgpgpxo-1.0.so.0 (0x00731000)
libart_lgpl_2.so.2 => /usr/lib/libart_lgpl_2.so.2 (0x003b0000)
libgpgf2-1.0.so.0 => /usr/lib/libgpgf2-1.0.so.0 (0x003ec000)
libgpg-1.0.so.0 => /usr/lib/libgpg-1.0.so.0 (0x00d12000)
libgobject-2.0.so.0 => /usr/lib/libgobject-2.0.so.0 (0x002a0000)
libgmodule-2.0.so.0 => /usr/lib/libgmodule-2.0.so.0 (0x002e7000)
libdb1-2.0 => /usr/lib/libdb1.so.2 (0x00c6f000)
liblib-2.0.so.0 => /usr/lib/liblib-2.0.so.0 (0x001f5000)
libfontconfig.so.1 => /usr/lib/libfontconfig.so.1 (0x0018e000)
libfreetype.so.6 => /usr/lib/libfreetype.so.6 (0x00101000)
libz.so.1 => /usr/lib/libz.so.1 (0x00d61000)
libpthread.so.0 => /lib/tls/libpthread.so.0 (0x00474000)
libc.so.6 => /lib/tls/libc.so.6 (0x00b0a000)
libX11.so.6 => /usr/lib/libX11.so.6 (0x0c7f1000)
libXrandr.so.2 => /usr/lib/lib/libXrandr.so.2 (0x0019ce000)
libX11.so.6 => /usr/lib/lib/libX11.so.6 (0x00383000)
libext.so.6 => /usr/lib/lib/libext.so.6 (0x0051000)
libXft.so.2 => /usr/lib/lib/libXft.so.2 (0x00d0b000)
libXrender.so.1 => /usr/lib/lib/libXrender.so.1 (0x004f4000)
/lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x00a0f1000)
libexpat.so.0 => /usr/lib/libexpat.so.0 (0x00a9d000)
```

In this case, the program uses quite a few shared libraries, including the X11 library (`libX11.so.6`), the GIMP toolkit (`libgtk-x11-2.0.so.0`), the *General Drawing Kit (GDK) library* (`libgdk-x11-2.0.so.0`), the *Math Library* (`libm.so.6`), and the C library (`libc.so.6`).

Almost any Linux application requires shared libraries to run.

#### Creating a shared library

Creating a shared library for your own application is fairly simple. Suppose you want to implement an object in the form of a shared library (think of an object as a bunch of code and data). A set of functions in the shared library represents the object's interfaces. To use the object, you load its shared library and invoke its interface functions. (I show you how to load a library in the following section.)

Here is the C source code for this simple object, implemented as a shared library (you might also call it a *dynamically linked library*) — save this code in a file named `dynobj.c`:

```c
/* ------------------------------------------------------------ */
/* File: dynobj.c
 *
 * Demonstrate use of dynamic linking.
 * Pretend this is an object that can be created by calling
 * init and destroyed by calling destroy.
 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

/* Data structure for this object */
typedef struct OBJDATA
{
    char *name;
    int version;
} OBJDATA;

/* ------------------------------------------------------------ */
/* init
 *
 * Initialize object (allocate storage).
 */
void* init(char *name)
{
    OBJDATA *data = (OBJDATA*)calloc(1, sizeof(OBJDATA));
    if(name)
        data->name = malloc(strlen(name)+1);
    strcpy(data->name, name);

    printf("Created: %s\n", name);

    return data;
}
/* ------------------------------------------------------------ */
```
