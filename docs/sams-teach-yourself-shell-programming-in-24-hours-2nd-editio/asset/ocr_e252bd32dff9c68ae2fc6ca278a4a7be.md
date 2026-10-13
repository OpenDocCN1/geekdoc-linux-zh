To embed integer calculations within a command, you can use the following syntax:

```
$((integer_expression))
```

# Integer Expression Operators

The integer operators are used to perform simple arithmetic operations on integer values.

The following list (order from highest to lowest operator precedence) describes the integer operators supported in ksh, bash and zsh. The logical operators described in this list return 1 for true and 0 for false.

+   - `-` unary minus (negates the following value)
+   - `!` logical NOT, binary one's complement
+   - `* / %` multiply, divide, modulus (remainder operation)
+   - `+ -` add, subtract
+   - `>> <<` right, left shift, for example: `$((32 >> 2))` gives 8 (right shift 32 by 2 bits is the same as division by 4)
+   - `<= >=` less than or equal to, greater than or equal to
+   - `> <` greater than, less than
+   - `== !=` equal to, not equal to
+   - `&` bitwise AND operation, for example: `$((5 & 3))` converts 5 to binary 101 and 3 to binary 011 and ANDs the bits to give 1 as the result
+   - `^` bitwise exclusive OR operation
+   - `|` bitwise regular OR operation
+   - `&&` logical AND
+   - `||` logical OR
+   - `*= /= %=` C programming type assignment, for example, `$((A *= 2))` means multiply variable A by 2, save result in A, and substitute result
+   - `+= -= ...` more C programming type assignments
+   - `>>= <<=` more C programming type assignments using shift right, shift left
+   - `&= ^= |=` more C programming type assignments using AND, exclusive OR, and regular OR

![](bbox=[0.85, 0.5, 0.98, 0.7])