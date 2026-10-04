# 760 Shared Libraries in Linux Applications

| Table 2-4 (continued) |
| Header File | Purpose |
| --- | --- |
| <string.h> | Declares the string manipulation routines such as strcmp and strcpy. |
| <time.h> | Defines data types and declares functions that manipulate them. Defines the types clock_t and time_t and the tm data structure. |
| <wchar.h> | Defines data types and declares functions for working with wide character data types (wchar_t). |
| <ctype.h> | Defines data types and declares functions for classifying and converting wide character data types (wchar_t). |

# Shared Libraries in Linux Applications

Most Linux programs use shared libraries. At a minimum, C programs use the C shared library 1ibc.so.X, where X is a version number. Using the shared library is desirable because many programs can share the same shared library—you need only one copy of the shared library loaded into memory. Also, the dynamic linking (where a program loads code modules and links with them at runtime) is becoming increasingly popular because it enables an application to load blocks of code only when needed, thus reducing the memory requirement of the application.

When a program uses one or more shared libraries, you need the program's executable file, as well as all the shared libraries, to run the program. In other words, your program doesn't run if all shared libraries are unavailable.

![](bbox=[0.15, 0.645, 0.235, 0.708])

If you select an application that uses shared libraries, make sure all necessary libraries are distributed with your software.

The subject of shared libraries is of interest to Linux programmers because use of shared libraries reduces the size of executables. In this section I briefly describe how to create and use a shared library in a sample program.

# Examining shared libraries that a program uses

Use the ldd utility to determine which shared libraries an executable program needs. The following ldd command to see the shared libraries used by a program (that was stored in GCC in the default file name a.out):

```
ldd a.out
```