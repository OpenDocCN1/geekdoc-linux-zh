# 12.3 Temporary Files

![](bbox=[0.08, 0.12, 0.92, 0.28])

For the reasons given, and others, all three functions described in this section should never be used. They exist in POSIX and in GLIBC only to support old programs that were written before the dangers of these routines were understood. To this end, GNU/Linux systems generate a warning at link time:

```
$ cc ch12-mkstemp.c -o ch12-mkstemp Compile the program
/tmp/cclXCvD9.o(.text+0x35): in function 'main':
: the use of `mkstemp' is dangerous, better use 'mkstemp'
(We cover mkstemp( ) in the next subsection.)
```

Should your system not have mkstemp( ), think about how you might use these interfaces to simulate it. (See also “Exercises” for Chapter 12, page 482, at the end of the chapter.)

# 12.3.2 Creating and Opening Temporary Files (Good)

There are two functions that don't have race condition problems. One is intended for use with the <stdio.h> library:

```
#include <stdio.h> ISO C
FILE *tmpfile(void);
```

The second function is for use with the file-descriptor-based system calls:

```
#include <stdlib.h> XSI
int mkstemp(char *template);
```