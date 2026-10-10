# Table 33.2	Tcl Operators

| Operator | Meaning | Operand Types |
| :--- | :--- | :--- |
| .x | Negative of x | Integer, Real |
| !x | Logical NOT: 1 if x is 0; 0 otherwise | Integer, Real |
| ~x | Bitwise complement of x | Integer |
| x*y | Product of x and y | Integer, Real |
| x/y | Quotient of x divided by y | Integer, Real |
| x%y | Remainder of x divided by y | Integer |
| x+y | Sum of x and y | Integer, Real |
| x-y | Difference of x minus y | Integer, Real |
| x<<y | Left-shift x by y bits | Integer |
| x>>y | Right-shift x by y bits | Integer |
| x<y | 1 if x is less than y; 0 otherwise | Integer, Real, String |
| x<=y | 1 if x is less than or equal to y; 0 otherwise | Integer, Real, String |
| x>y | 1 if x is greater than y; 0 otherwise | Integer, Real, String |
| x>=y | 1 if x is greater than or equal to y; 0 otherwise | Integer, Real, String |
| x==y | 1 if x equals y; 0 otherwise | Integer, Real, String |
| x!=y | 1 if x does not equal y; 0 otherwise | Integer, Real, String |
| x&y | Bitwise-AND of x and y | Integer |
| x^y | Bitwise exclusive-OR of x and y | Integer |
| x|y | Bitwise-OR of x and y | Integer |
| x&&y | Logical AND of x and y: 1 if both are non-zero; 0 otherwise | Integer |
| x||y | Logical OR of x and y: 1 if either is non-zero; 0 otherwise | Integer |
| x?y:z | Choice: y if x is non-zero; otherwise z | Integer, Real |

As in C, the logical operators are short-circuit operators. If the first operand of `&&` is zero, or the first operand of `||` is non-zero, the second operand is not evaluated.

Within an expression, substitution occurs through the normal parser mechanism.
However, the expression evaluator also performs variable substitution. Consider the following example:

```
% set a 5
5
% expr 5+$a
10
% expr {$a+$a}
10
```