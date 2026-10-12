| E | acerb |
| S |       |

The c function is identical to the $ function up through the end of the w loop. When the w loop is exited, the function analyzes the two characters that resulted in the termination of the w loop. If s is less than s, s must be lexicographically less than s. In such a case, $1 is returned. If s is equal to s, the two strings are equal so 0 is returned. If neither is true, s must be lexicographically greater than s, in which case 1 is returned.

The l function defines i variables l and h and assigns them initial values defined by the binary search algorithm. The w loop executes as long as l does not exceed h. Inside the loop, the value m is calculated by adding l and h and dividing the result by 2. The c function is then called with the word contained in d and the word you are searching for as arguments. The returned value is assigned to the variable r.

If c returns a value of -1—indicating that d is less than s, -1 sets the value of l to m + 1. If c returns 1—indicating that d is greater than s, -1 sets the value of h to m - 1. If neither -1 nor 1 is returned, the two strings must be equal, and, in that case, l returns the value of m, which is the entry number of the word in the dictionary.

If l eventually exceeds h, the word is not in the dictionary. In that case, l returns -1 to indicate this “not found” condition.

# ## Character Operations

Character variables and constants are frequently used in relational and arithmetic expressions. To properly use characters in such situations, it is necessary for you to understand how they are handled by the C compiler.

Whenever a character constant or variable is used in an expression in C, it is automatically converted to, and subsequently treated as, an integer value.

In Chapter 5, “Making Decisions,” you saw how the expression

```
```C
c
```
```

could be used to determine if the character variable c contained a lowercase letter. As mentioned there, such an expression could be used on systems that used an ASCII character representation because the lowercase letters are represented sequentially in ASCII, with no other characters in-between. The first part of the preceding expression, which compares the value of c against the value of the character constant ' , is actually comparing the value of c against the internal representation of the character ' . In ASCII, the character ' has the value 9 , the character ' has the value 9 , and so on. Therefore, the expression c is TRUE (nonzero) for any lowercase character contained in c because it has a value that is greater than or equal to 97. However, because there are