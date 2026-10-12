Counts the maximum number of initial characters in *s1* that consist only of characters from *s2*, returning the result.

c             (*s1, *s2*)

Searches the string *s1* for the first occurrence of the string *s2*. If found, a pointer to the start of where *s2* is located inside *s1* is returned; otherwise, if *s2* is not located inside *s1*, the null pointer is returned.

c             (*s1, *s2*)

Breaks the string *s1* into tokens based on delimiter characters in *s2*. For the first call, *s1* is the string being parsed and *s2* contains a list of characters that delimit the tokens. The function places a null character in *s1* to mark the end of each token as it is found and returns a pointer to the start of the token. On subsequent calls, *s1* should be a null pointer. When no more tokens remain, a null pointer is returned.

s             (*s1, *s2, n*)

Transforms up to *n* characters from the string *s2*, placing the result in *s1*. Two such transformed strings from the current locale can then be compared with s.

# Memory Functions

The following routines deal with arrays of characters. They are designed for efficient searching of memory and for copying data from one area of memory to another. They require the header file `<string.h>`:

```
#include <string.h>
```

In the description of these routines, *m1* and *m2* are of type v, *c* is an i that gets converted by the routine to an u, and *n* is an integer of type s.

v             (*m1, c, n*)

Searches *m1* for the first occurrence of *c*, returning a pointer to it if found, or the null pointer, if not found after examining *n* characters.

v             (*m1, *m2, n*)

Compares the corresponding first *n* characters from *m1* and *m2*. Zero is returned if both arrays are identical in their first *n* characters. If they’re not, the difference between the corresponding characters from *m1* and *m2* that caused the first mismatch is returned. So, if the disagreeing character from *m1* was less than the corresponding character from *m2*, a value less than zero is returned; otherwise, a value greater than zero is returned.

v             (*m1, *m2, n*)

Copies *n* characters from *m2* to *m1*, returning *m1*.

v             (*m1, *m2, n*)

Is like m, but is guaranteed to work even if *m1* and *m2* overlap in memory.

v             (*m1, c, n*)