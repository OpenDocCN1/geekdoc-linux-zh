# # Handling Errors in Your C Program

ESSL provides you with flexibilities in handling both input-argument errors and computational errors:

+   * For input-argument errors 2015, 2030, and 2200, which are optionally-recoverable errors, ESSL allows you to obtain corrected input-argument values and react at run time.

+   **Note:** In the case where error 2015 is unrecoverable, you have the option of dynamic allocation for most of the *aux* arguments. For details see the subroutine descriptions in Part 2 of this book.

+   * For computational errors, ESSL provides a return code and additional information to help you analyze the problem in your program and react at run time.

*“Input-Argument Errors in C” and “Computational Errors in C” on page 136 explain how to use these facilities by describing the additional statements you must code in your program.*

For multithreaded application programs, if you want to initialize the error option table and change the default settings for input-argument and computational errors, you need to implement the steps shown in *Input-Argument Errors in C* and *Computational Errors in C* on page 136 on each thread that calls ESSL.

# ## Input-Argument Errors in C

To obtain corrected input-argument values in a C program and to avert program termination for the optionally-recoverable input-argument errors 2015, 2030, and 2200, add the statements in the following steps to your program. Steps 4 and 8 for ERRSAV and ERRSTR, respectively, are optional. Adding these steps makes the effect of the call to ERRSET temporary.

**Step 1. Code the Global Statements for ESSL Error Handling:**

```
```c
/* Code two underscores */
/* before the letters ESVER */
#define __ESVERR
#include <essl.h>
extern int enotrm();
```
```

These statements are coded with your global declares in the front of your program. The `#define` must be coded before the `#include` statement for the ESSL header file. The *extern* statement declares the ESSL error exit routine ENOTRM as an external reference in your program. **After the point where you code these statements in your program, you must pass by reference all ESSL calling sequence arguments that can potentially be altered by ESSL error handling. This applies to all your ESSL call statements. The two types of arguments are:**

+   * *aux* arguments for auxiliary storage
+   * *n* arguments for transform lengths