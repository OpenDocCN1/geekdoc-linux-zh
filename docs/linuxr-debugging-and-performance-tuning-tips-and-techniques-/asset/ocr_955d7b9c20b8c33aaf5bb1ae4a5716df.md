# 3.2 Memory Allocation

```
#include <string.h>

/* strdup --- malloc() storage for a copy of string and copy it */
char *strdup(const char *str)
{
    size_t len;
    char *copy;

    len = strlen(str) + 1;    /* include room for terminating `\0' */
    copy = malloc(len);
    if (copy != NULL)
        strcpy(copy, str);

    return copy;            /* returns NULL if error */
}
```

With the 2001 POSIX standard, programmers the world over can breathe a little easier: This function is now part of POSIX as an XSI extension:

```
#include <string.h>                          XSI

char *strdup(const char *str);            Duplicate str
```

The return value is NULL if there was an error or a pointer to dynamically allocated storage holding a copy of *str*. The returned value should be freed with free() when it’s no longer needed.

# 3.2.3 System Calls: brk() and sbrk()

The four routines we’ve covered (malloc(), calloc(), realloc(), and free()) are the standard, portable functions to use for dynamic memory management.

On Unix systems, the standard functions are implemented on top of two additional, very primitive routines, which directly change the size of a process’s address space. We present them here to help you understand how GNU/Linux and Unix work (“under the hood” again); it is highly unlikely that you will ever need to use these functions in a regular program. They are declared as follows:

```
#include <unistd.h>          Common
#include <malloc.h>          /* Necessary for glibc 2 systems */

int brk(void *end_data_segment);
void *sbrk(ptrdiff_t increment);
```