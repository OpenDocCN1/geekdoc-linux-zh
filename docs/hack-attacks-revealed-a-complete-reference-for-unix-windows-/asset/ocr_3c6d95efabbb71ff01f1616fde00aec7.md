# Pointers

A pointer is a variable that holds the memory address of an item of data. A pointer is declared like an ordinary variable, but its name is prefixed by an asterisk (*), as illustrated here:

```
char  *p;
```

This example declares the variable p to be a pointer to a character variable.

Pointers are very powerful, and similarly dangerous, because a pointer can be inadvertently set to point to the code segment of a program, and then some value can be assigned to the address of the pointer. The following program illustrates a simple pointer application:

```
#include <stdio.h>

main()
{
   int a;
   int *x;

   /* x is a pointer to an integer data type */

   a = 100;
   x = &a;

   printf ("\nVariable 'a' holds the value %d at memory address %p", a,*x);
}
```

Pointers may be incremented and decremented and have other mathematics applied to them as well. Pointers are commonly used in dynamic memory allocation. When a program is running, it is often necessary to temporarily allocate a block of data in memory. C provides the function malloc() for this purpose; it follows the general form:

```
any pointer type = malloc(number_of_bytes);
```

Here, malloc() actually returns a void pointer type, which means it can be any type—integer, character, floating point, and so on. This example allocates a table in memory for 1,000 integers:

```
#include <stdio.h>
#include <stdlib.h>

main()
{
   int *x;
   int n;

   /* x is a pointer to an integer data type */

   /* Create a 1000 element table, sizeof() returns the compiler */
   /* specific number of bytes used to store an integer */

   x = malloc(1000 * sizeof(int));
```