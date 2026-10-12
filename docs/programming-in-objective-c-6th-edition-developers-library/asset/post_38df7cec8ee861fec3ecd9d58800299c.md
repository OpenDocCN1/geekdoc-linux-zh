
The `restrict` keyword can be used with pointers. It is a hint to the compiler for optimization (like the `const` keyword for variables). The `restrict` keyword specifies to the compiler that the pointer is the only reference to a particular object; that is, it is not referenced by any other pointer within the same scope. The lines:

```c
int *restrict i;
int *restrict j;
```

tell the compiler that for the duration of the scope in which `i` and `j` are defined, they will never access the same value. Their use for pointing to integers (in an array, for example) is mutually exclusive.

## 5.0 Expressions

Variable names, function names, array names, constants, function calls, array references, and structure and union references are all considered expressions. Applying a unary operator (where appropriate) to one of these expressions is also an expression, as is combining two or more of these expressions with a binary or ternary operator. Finally, an expression enclosed within parentheses is also an expression.

An expression of any type other than `void` that identifies a data object is called an `lvalue`. If it can be assigned a value, it is known as a `modifiable lvalue`.

Modifiable lvalue expressions are required in certain places. The expression on the left-hand side of an assignment operator must be a modifiable lvalue. Furthermore, the increment and decrement operators can only be applied to modifiable lvalues, as can the unary address operator `&` (unless it’s a function).

## 5.1 Summary of C Operators

Table A.5 summarizes the various operators in the C language. These operators are listed in order of decreasing precedence. Operators grouped together have the same precedence.

| Operator | Description | Associativity |
| :--- | :--- | :--- |
| `()` | Function call | |
| `[]` | Array element reference | |
| `->` | Pointer to structure member reference | Left to right |
| `.` | Structure member reference | |
| `-` | Unary minus | |
| `+` | Unary plus | |
| `++` | Increment | |
| `--` | Decrement | |
| `!` | Logical negation | |
| `~` | Ones complement | Right to left |
| `*` | Pointer reference (indirection) | |
| `&` | Address | |
| `sizeof` | Size of an object | |
| `(type)` | Type cast (conversion) | |
| `*` | Multiplication | |
| `/` | Division | Left to right |
| `%` | Modulus | |
| `+` | Addition | Left to right |
| `-` | Subtraction | |
| `<<` | Left shift | Left to right |
| `>>` | Right shift | |
| `<` | Less than | |
| `<=` | Less than or equal to | Left to right |
| `>` | Greater than | |
| `>=` | Greater than or equal to | |
| `==` | Equality | Left to right |
| `!=` | Inequality | |
| `&` | Bitwise AND | Left to right |
| `^` | Bitwise XOR | |
| `\|` | Bitwise OR | Left to right |
| `&&` | Logical AND | Left to right |
| `\|\|` | Logical OR | Left to right |
| `? :` | Conditional | Right to left |
| `=` | Assignment operators | Right to left |
| `*=` `/=` `%=` | | |
| `+=` `-=` `&=` | | |
| `^=` `\|=` | | |
| `<<=` `>>=` | | |
| `,` | Comma operator | Right to left |

**Table A.5 Summary of C Operators**

As an example of how to use Table A.5, consider the following expression:

```c
a & b | c
```

The multiplication operator has higher precedence than both the bitwise OR and bitwise AND operators because it appears above both of these in Table A.5. Similarly, the bitwise AND operator has higher precedence than the bitwise OR operator because the former appears above the latter in the table. Therefore, this expression is evaluated as:

```c
(a & b) | c
```

Now consider the following expression:

```c
a % b * c
```

Because the modulus and multiplication operator appear in the same grouping in Table A.5, they have the same precedence. The associativity listed for these operators is left to right, indicating that the expression is evaluated as:

```c
(a % b) * c
```

As another example, the expression:

```c
-a + b
```

is evaluated as:

```c
(-a) + b
```

because the `-` operator has higher precedence than the `+` operator.

Finally, because the assignment operators group from right to left, the statement:

```c
a = b = 0
```

is evaluated as:

```c
a = (b = 0)
```

which has the net result of setting the values of `a` and `b` to 0. In the case of the expression:

```c
i++ + x
```

it is not defined whether the compiler evaluates the left side of the plus operator or the right side first. Here, the way that it’s done affects the result because the value of `i` might be incremented before `x` is evaluated.

Another case in which the order of evaluation is not defined is in the following expression:

```c
x[i++]
```

In this situation, it is not defined whether the value of `i` is incremented before or after its value is used to index into `x`.

The order of evaluation of function arguments is also undefined. Therefore, in the function call:

```c
f(i++, i++)
```

`i` might be incremented first, thereby causing the same value to be sent as the two arguments to the function.

The C language guarantees that the `&&` and `||` operators are evaluated from left to right. Furthermore, in the case of `&&`, it is guaranteed that the second operand is not evaluated if the first is 0; and in the case of `||`, it is guaranteed that the second operand is not evaluated if the first is nonzero. This fact is worth bearing in mind when forming expressions such as:

```c
if (d == 0 && c()) { ... }
```

because, in this case, `c` is called only if the value of `d` is 0. To take another example, if the array `a` is defined to contain `n` elements, the statement that begins:

```c
i < n && a[i] == 0
```

references the element contained in the array only if `i` is a valid subscript in the array.

## 5.2 Constant Expressions

A constant expression is an expression in which each of the terms is a constant value. Constant expressions are required in the following situations:

- As the value after a `case` in a `switch` statement
- For specifying the size of an array that is initialized or globally declared
- For assigning a value to an enumeration identifier
- For specifying the bit field size in a structure definition
- For assigning initial values to `static` variables
- For assigning initial values to global variables
- As the expression following the `#` in a `#` preprocessor statement

In the first four cases, the constant expression must consist of integer constants, character constants, enumeration constants, and size expressions. The only operators that can be used are the arithmetic operators, the bitwise operators, the relational operators, the conditional expression operator, and the type cast operator. The `sizeof` operator cannot be used on an expression with a variable-length array because the result is evaluated at runtime and is, therefore, not a constant expression.

In the fifth and sixth cases, in addition to the rules cited earlier, the address operator can be implicitly or explicitly used. However, it can only be applied to global or `static` variables or functions. So, for example, the expression:

```c
&x
```

is a valid constant expression, provided that `x` is a global or `static` variable. Furthermore, the expression:

```c
&a
```

is a valid constant expression if `a` is a global or `static` array. Finally, because `&a` is equivalent to the expression `a`, `a` is also a valid constant expression.

For the last situation that requires a constant expression (after the `#`), the rules are the same as for the first four cases, except the `sizeof` operator, enumeration constants, and the type cast operator cannot be used. However, the special `sizeof` operator is permitted (see Section 9.2.3).

## 5.3 Arithmetic Operators

Given that:

```c
a, b, c, d, e, f
```

are expressions of any basic data type except `void`;

```c
i, j
```

are expressions of any integer data type;

then the expression:

- `-a` negates the value of `a`
- `+a` gives the value of `a`
- `a + b` adds `a` with `b`
- `a - b` subtracts `b` from `a`
- `a * b` multiplies `a` by `b`
- `a / b` divides `a` by `b`
- `i % j` gives the remainder of `i` divided by `j`

In each expression, the usual arithmetic conversions are performed on the operands (see Section 5.17). If `a` is unsigned, `-a` is calculated by first applying integral promotion to it, subtracting it from the largest value of the promoted type, and adding `1` to the result.

If two integral values are divided, the result is truncated. If either operand is negative, the direction of the truncation is not defined (that is, $-3 \div 2$ might produce $-1$ on some machines and $-2$ on others); otherwise, truncation is always toward zero ($3 \div 2$ always produces $1$). See Section 5.15 for a summary of arithmetic operations with pointers.

## 5.4 Logical Operators

Given that:

```c
a, b
```

are expressions of any basic data type except `void`, or are both pointers,

then the expression:

- `a && b` has the value `1` if both `a` and `b` are nonzero, and `0` otherwise (and `b` is evaluated only if `a` is nonzero)
- `a || b` has the value `1` if either `a` or `b` is nonzero, and `0` otherwise (and `b` is evaluated only if `a` is zero)
