# B. The Standard C Library

The standard C library contains a large selection of functions that might be called from a C program. This section does not list all of these functions, but rather most of the more commonly used ones. For a complete listing of all the functions that are available, consult the documentation that was included with your compiler, or check one of the resources listed in Appendix E, “Resources.”

Among the routines not described in this appendix are ones for manipulating the date and time (such as time, clock, and local time), performing nonlocal jumps (setjump and longjmp), generating diagnostics (assert), handling a variable number of arguments (va_start, va_arg, va_end, and va_copy), handling signals (signal and raise), dealing with localization (as defined in <locale.h>), and dealing with wide character strings.

# Standard Header Files

This section describes the contents of some standard header files: <stdio.h>, <stdlib.h>, <string.h>, <ctype.h>, and <locale.h>.

# stdio.h

This header file contains some standard definitions, such as the following:

| Define | Meaning |
| :--- | :--- |
| NULL | A null pointer constant |
| offsetof (structure, member) | The offset in bytes of the member member from the start of the structure structure; the type of the result is size_t |
| ptrdiff_t | The type of integer produced by subtracting two pointers |
| size_t | The type of integer produced by the sizeof operator |
| wchar_t | The type of the integer required to hold a wide character (see Appendix A, “C Language Summary”) |

# limits.h

This header file contains various implementation-defined limits for character and integer data types. Certain minimum values are guaranteed by the ANSI standard. These are noted at the end of each description inside parentheses.