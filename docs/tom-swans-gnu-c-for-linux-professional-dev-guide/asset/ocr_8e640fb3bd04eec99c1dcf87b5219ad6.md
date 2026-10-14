There's no practical limit to a string's size, and it's often useful to use them for large buffers, perhaps for performing "raw" disk operations. The following declares a buffer of 1,028 bytes:

```
char buffer[1028];
```

# Warning

> Never create large string variables or buffers inside functions! This places the variable on the relatively limited system stack and is not good programming. See Chapter 11, "Managing Memory with Pointers," for other ways to create string variables and large buffers without using global declarations.

Because C-style string variables are actually arrays of individual characters, you cannot assign new strings to them using assignment statements. The following does not work:

```
pathname = "/etc/scripts"; // ???
```

That fails to compile because the assignment operator is not defined for C-style string variables. To copy one C-style string to another requires calling a standard string function, such as strcpy(). To do that, include the standard string.h header file with the following directive:

```
#include <string.h>
```

You can then call strcpy() to copy a string into the variable using a statement such as

```
strcpy(pathname, "/usr/yourname");
```

That copies "/usr/yourname" into pathname. Be careful that the source string isn't larger than the target variable. A similar, but safer, function, strncpy(), limits how many characters are copied. If source and destination are the names of C-style string variables, the following statement copies up to 10 characters from source to destination:

```
strncpy(destination, source, 10);
```

# Note

> Generally, string functions with an extra n in their names declare a numeric parameter that limits the function's action in some way. These functions tend to be safer or more restrictive than their n-less counterparts. Examples include strcpy() and strncpy(), strcat() and strncat(), and strcmp() and strncmp(). See the info pages for online documentation on these functions.

# SIZE MATTERS

The size of a string determines how many characters it can hold. The length of a string is equal to how many characters the string currently holds. Listing 6.10 demonstrates the difference between string size and length.