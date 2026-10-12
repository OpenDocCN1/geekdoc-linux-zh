
Removes the specified file. A nonzero value is returned on failure.

Renames the file *fileName1* to *fileName2*, returning a nonzero result on failure.

Resets the indicated file back to the beginning.

Reads items from *s* according to the format specified by the string *format* (see [Chapter 15](#15)). The arguments that follow *format* must all be pointers. The number of items successfully read and assigned (excluding % assignments) is returned by the function. The value *E* is returned if an end of file is encountered before any items have been converted.

Creates and opens a temporary binary file in write update mode ("w+b"); it returns *N* if an error occurs. The temporary file is automatically removed when the program terminates. (A function called *t* is also available for creating unique, temporary file names.)

Effectively “puts back” a character to the indicated file. The character is not actually written to the file but is placed in a buffer associated with the file. The next call to *g* returns this character. The *u* function can only be called to “put back” one character to a file at a time; that is, a read operation must be performed on the file before another call to *u* can be made. The function returns *c* if the character is successfully “put back”; otherwise, it returns the value *E*.

## In-Memory Format Conversion Functions

The functions *s* and *s* are provided for performing data conversion in memory. These functions are analogous to the *f* and *f* functions, except a character string replaces the *F* pointer as the first argument. You should include the header file `<stdio.h>` in your program when using these routines.

The specified arguments are converted according to the format specified by the character string *format* (see [Chapter 15](#15)) and are placed into the character array pointed to by *buffer*. A null character is automatically placed at the end of the string inside *buffer*. The number of characters placed into *buffer* is returned, excluding the terminating null. As an example, the code

results in the character string "100" being stored in *f*.

```
i buffer, format, arg1, arg2, ..., argn)
```

The values as specified by the character string format are read from buffer and stored in the corresponding pointer arguments that follow format (see Chapter 15). The number of items successfully converted is returned by this function. As an example, the code

stores the string "55" inside *m*, the integer value 1 inside *d*, and the integer value 2 inside *y*. The code

converts the first command-line argument (pointed to by *a*) to a floating-point number, and checks the value returned by *s* to see if a number was successfully read from *a*. (See the routines described in the next section for other ways to convert strings to numbers.)

### String-to-Number Conversion

The following routines convert character strings to numbers. To use any of the routines described here, include the header file `<stdlib.h>` in your program.

In the descriptions that follow, *s* is a pointer to a null-terminated string, *end* is a pointer to a character pointer, and *base* is an *int*.

All routines skip leading whitespace characters in the string and stop their scan upon encountering a character that is invalid for the type of value being converted.

```
double strtod(const char *s, char **end)
```
Converts the string pointed to by *s* into a floating-point number, returning the result.

```
int strtoimax(const char *s, char **end, int base)
```
Converts the string pointed to by *s* into an *intmax_t*, returning the result.

```
long strtol(const char *s, char **end, int base)
```
Converts the string pointed to by *s* into a *long*, returning the result.

```
long long strtoll(const char *s, char **end, int base)
```
Converts the string pointed to by *s* into a *long long*, returning the result.

```
double strtod(const char *s, char **end)
```
Converts *s* to *double*, returning the result. A pointer to the character that terminated the scan is stored inside the character pointer pointed to by *end*, provided *end* is not a null pointer. As an example, the code

has the effect of storing the value 12.5 inside *v*. The character pointer variable *p* is set by *strtod* to point to the character in *buffer* that terminated the scan. In this case, it is set pointing to the character `'.'`.

```
float strtof(const char *s, char **end)
```
Is like *strtod*, except converts its argument to *float*.

```
int strtol(const char *s, char **end, int base)
```
Converts *s* to *long*, returning the result. *base* is an integer base number between 2 and 36, inclusive. The integer is interpreted according to the specified base. If *base* is 0, the integer can be expressed in either base 10, octal (leading 0), or hexadecimal (leading 0x or 0X). If *base* is 16, the value can optionally be preceded by a leading 0x or 0X. A pointer to the character that terminated the scan is stored inside the character pointer pointed to by *end*, provided *end* is not a null pointer.

```
long long strtoll(const char *s, char **end, int base)
```
Is like *strtol*, except converts its argument to *long long*.

```
unsigned int strtoul(const char *s, char **end, int base)
```
Is like *strtol*, except an *unsigned int* is returned.

```
unsigned long strtoul(const char *s, char **end, int base)
```
Converts *s* to *unsigned long*, returning the result. The remaining arguments are interpreted as for *strtol*.

```
unsigned long long strtoull(const char *s, char **end, int base)
```
Converts *s* to *unsigned long long*, returning the result. The remaining arguments are interpreted as for *strtol*.

## Dynamic Memory Allocation Functions

The following functions are available for allocating and freeing memory dynamically. For each of these functions, *n* and *size* represent integers of type *size_t*, and *pointer* represents a *void* pointer. To use these functions, include the following line in your program:

```
#include <stdlib.h>
```

```
void *malloc(size_t n, size_t size)
```
Allocates contiguous space for *n* items of data, where each item is *size* bytes in length. The allocated space is initially set to all zeroes. On success, a pointer to the allocated space is returned; on failure, the null pointer is returned.

```
void free(void *pointer)
```
Returns a block of memory pointed to by *pointer* that was previously allocated by a *calloc*, *malloc*, or *realloc* call.

```
void *calloc(size_t n, size_t size)
```
Allocates contiguous space of *n* *size* bytes, returning a pointer to the beginning of the allocated block if successful, and the null pointer otherwise.

```
void *realloc(void *pointer, size_t size)
```
Changes the size of a previously allocated block to *size* bytes, returning a pointer to the new block (which might have moved), or a null pointer if an error occurs.

## Math Functions

The following list identifies the math functions. To use these routines, include the following statement in your program:

```
#include <math.h>
```

The standard header file `<tgmath.h>` defines type-generic macros that can be used to call a function from the math or complex math libraries without worrying about the argument type. For example, you can use six different square root functions based upon the argument type and return type:

- `double sqrt(double)`
- `float sqrtf(float)`
- `long double sqrtl(long double)`
- `double complex csqrt(double complex)`
- `float complex csqrtf(float complex)`
- `long double complex csqrtl(long double complex)`

Instead of having to worry about all six functions, you can include `<tgmath.h>` instead of `<math.h>` and `<complex.h>` and just use the “generic” version of the function under the name *sqrt*. The corresponding macro defined in `<tgmath.h>` ensures that the correct function gets called.

Returning to `<tgmath.h>`, the following macros can be used to test specific properties of floating-point values given as argument(s):

- Classifies $x$ as NaN, infinite, normal, subnormal, zero, or in some other implementation-defined category; each value is defined in `<math.h>`
- Does $x$ represent a finite value?
- Does $x$ represent an infinite value?
- Is $x > y$?
- Is $x \geq y$?
- Is $x \leq y$?
- Is $x < y$ or is $x > y$?
- Is $x$ a NaN (that is, not a number)?
- Is $x$ a normal value?
- Are $x$ and $y$ unordered (for example, one or both might be NaNs)?
- Is the sign of $x$ negative?

In the list of functions that follows, $x$, $y$, and $z$ are of type *double*, $r$ is an angle expressed in radians and is of type *double*, and $n$ is an *int*.

For more information about how errors are reported by these functions, consult your documentation.

1. The math library contains *float*, *double*, and *long double* versions of the math functions that take and return *float*, *double*, and *long double* values. The *double* versions are summarized here. The *float* versions have the same name with an f on the end (e.g. *acosf*). The *long double* versions have an l on the end instead (e.g. *acosl*).

```
double acos(double x)
```
Returns the arccosine of $x$, as an angle expressed in radians in the range $[0, \pi]$. $x$ is in the range $[-1, 1]$.
