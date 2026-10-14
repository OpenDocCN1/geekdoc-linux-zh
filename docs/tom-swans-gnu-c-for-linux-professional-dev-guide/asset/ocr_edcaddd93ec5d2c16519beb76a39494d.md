The first command compiles main.cpp, creating main.o. The second command compiles first.cpp and second.cpp, creating the object code files first.o and second.o. Finally, the third command specifies runme as the output code filename and links the three object code files along with any needed library code to create the finished program. In the third command, g++ is used merely as an executive—a kind of supervisor—for running the linker. Because no source files are specified, the preprocessor, compiler, and assembler stages are skipped. It is possible to run the GNU linker directly, but using g++ as an executive usually easier and ensures that all proper linking options are selected.

# TO QUOTE OR NOT TO QUOTE

Programmers new to C or C++ are usually confused when writing #include directives whether to quote header filenames as in "header.h" or to bracket them like this: <header.h>. But the mystery is easily explained by two rules:

+   - Use brackets to include standard C and C++ header files such as iostream.h and stdlib.h.
+   - Use double quotes to include your own program’s header files. You may name them as you like, but it’s common to use the .h filename extension.

Most programs use a mix of standard and program headers. For example, the following two directives include two header files:

```
#include <time.h>
#include "graphics.h"
```

In the first instance, the compiler looks in its standard paths for the bracketed time.h file. In the second instance, the compiler looks for a file named graphics.h in the current directory.

# INCLUDE-FILE OPTIONS

Several useful options alter the directories where the compiler searches for files named in #include directives. By using these options, you can tell the compiler to look in alternate directories for your program’s header files. Wild and crazy programmers cleverly name their include directories include.

The option -I (it must be a capital I) tells the compiler to search a named directory ahead of those it normally examines for quoted header files in directives such as

```
#include "myheader.h"
```

The following command, for example, tells the compiler to search in the /include directory for the program’s quoted header files before searching the current directory.

```
$ g++ -I /include attest.cpp
```

If you specify multiple directories using -I options, they are scanned in left-to-right order. The following command looks in two directories, include1 and include2, for the program’s quoted header files:

```
$ g++ -I /include1 -I /include2 attest.cpp
```