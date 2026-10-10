# 712 Expressions

| **Table 2-2 (continued)** | | |
| :--- | :--- | :--- |
| **Name of Operator** | **Syntax** | **Result** |
| **Relational and Logical Operators** | | |
| Equal to | x==y | Value is 1 if x equals y; otherwise, value is 0. |
| Not equal to | x!=y | Value is 1 if x and y are unequal; otherwise, value is 0. |
| Logical NOT | !x | Value is 1 if x is 0; otherwise, value is 0. |
| Logical AND | x&&y | Value is 0 if either x or y is 0. |
| Logical OR | x||y | Value is 0 if both x and y are 0. |
| **Assignment Operators** | | |
| Assignment | x=y | Places the value of y into x |
| Compound Assignment | x O=y | Equivalent to x = x O y, where O is one of the following operators: +, -, *, /, %, <, >, &, ^, or | |
| **Data Access and Size Operators** | | |
| Subscript | x[y] | Selects the y-th element of array x |
| Member selection | x.y | Selects member y of structure (or union) x |
| Member selection | x->y | Selects the member named y from a structure or union with x as its address |
| Indirection | *x | Contents of the location with x as its address |
| Address of | &x | Address of the data object named x |
| Size of | sizeof(x) | Size (in bytes) of the data object named x |
| **Bitwise Operators** | | |
| Bitwise NOT | ~x | Changes all 1s to 0s and 0s to 1s |
| Bitwise AND | x&y | Result is the bitwise AND of x and y. |
| Bitwise OR | x|y | Result is the bitwise OR of x and y. |
| Bitwise exclusive OR | x^y | Result contains 1s where corresponding bits of x and y differ. |
| Left shift | x<<y | Shifts the bits of x to the left by y bit positions. Fills 0s in the vacated bit positions. |
| Right shift | x>>y | Shifts the bits of x to the right by y bit positions. Fills 0s in the vacated bit positions. |