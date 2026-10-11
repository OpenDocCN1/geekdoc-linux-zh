Finally, you can combine all these kinds of values (constants, function calls, column references, and subqueries) to form more complex expressions.

# ### 3.5.1.1  Operator Types

Terms of expressions can be combined using several kinds of operators. This section describes what they do, and Section 3.5.1.2, “Operator Precedence,” discusses the order in which they are evaluated.

Arithmetic operators, listed in Table 3.18, include the usual addition, subtraction, multiplication, and division operators, as well as the modulo operator. Arithmetic is performed using `BIGINT` (64-bit) integer values for `+`, `-`, and `*` when both operands are integers. If both operands are integers, the result is unsigned if either operand is unsigned. For each operator other than `DIV`, if any operand is an approximate value, double-precision floating-point arithmetic is used. This is also true for strings converted to numbers, because strings are converted to double-precision numbers. Be aware that if an integer operation involves large values such that the result exceeds 64-bit range, you will get unpredictable results. (Actually, you should try to avoid exceeding 63-bit values; one bit is needed to represent the sign.)

**Table 3.18**  **Arithmetic Operators**

| Operator | Syntax | Meaning |
| :--- | :--- | :--- |
| + | `a + b` | Addition; sum of operands |
| - | `a - b` | Subtraction; difference of operands |
| - | `-a` | Unary minus; negation of operand |
| * | `a * b` | Multiplication; product of operands |
| / | `a / b` | Division; quotient of operands |
| DIV | `a DIV b` | Division; integer quotient of operands |
| % | `a % b` | Modulo; remainder after division of operands |


Logical operators, shown in Table 3.19, evaluate expressions to determine whether they are true (non-zero) or false (zero). It is also possible for a logical expression to evaluate to `NULL` if its value cannot be ascertained. For example, `1 AND NULL` is of indeterminate value.

**Table 3.19**  **Logical Operators**

| Operator | Syntax | Meaning |
| :--- | :--- | :--- |
| AND, && | `a AND b`, `a && b` | Logical intersection; true if both operands are true |
| OR, \|\| | `a OR b`, `a \|\| b` | Logical union; true if either operand is true |
| XOR | `a XOR b` | Logical exclusive-OR; true if exactly one operand is true |
| NOT, ! | `NOT a`, `!a` | Logical negation; true if operand is false |