Table 2-4 (continued)

| Header File | Purpose |
|---|---|
| `<time.h>` | Defines data types and declares functions that manipulate time. Defines the types `clock_t` and `time_t` and the tm data structure. |
| `<wchar.h>` | Defines data types and declares functions for working with wide character data types (`wchar_t`). |
| `<wctype.h>` | Defines data types and declares functions for classifying and converting wide character data types (`wchar_t`). |

# Shared Libraries in Red Hat Linux Applications

Most Red Hat Linux programs use shared libraries. At minimum, most C programs use the C shared library `libc.so.X`, wherein X is a version number. Using shared libraries is desirable because many executable programs can share the same shared library — you need only one copy of the shared library loaded into memory. Also, the dynamic linking (wherein a program loads code modules and links with them at runtime) is becoming increasingly popular because it enables an application to load blocks of code only when needed, thus reducing the memory requirement of the application.

When a program uses one or more shared libraries, you need the program's executable file, as well as all the shared libraries, to run the program. In other words, your program won't run if all shared libraries are not available on a system.

![](bbox=[0.15, 0.7, 0.25, 0.85])

If you sell an application that uses shared libraries, make sure all necessary shared libraries are distributed with your software.

The subject of shared libraries is of interest to Red Hat Linux programmers because use of shared libraries reduces the size of executables. In this section I briefly describe how to create and use a shared library in a sample program.

# Examining shared libraries that a program uses

Use the `ldd` utility to determine which shared libraries an executable program needs. Type the following `ldd` command to see the shared libraries used by a program (that was stored by GCC in the default file named `a.out`):

```
ldd a.out
```