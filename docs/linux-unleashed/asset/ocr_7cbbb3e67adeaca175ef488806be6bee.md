# Numbers

Perl stores all numeric data as floating-point values. You can use integers in your Perl programs, but Perl treats them all as floating-point numbers.

Perl provides a set of operators that can be used to perform comparisons between two numeric values and for performing the standard mathematical operations on numbers. Table 28.1 lists some of the operators that Perl provides for numeric data.

**TABLE 28.1. NUMERIC OPERATORS.**

| Operator | Description |
| :--- | :--- |
| `$a = op1 + op2` | Stores the value of op1 plus op2 into `$a` |
| `$a = op1 - op2` | Stores the value of op1 minus op2 into `$a` |
| `$a = op1 * op2` | Stores the value of op1 times op2 into `$a` |
| `$a = op1 / op2` | Stores the value of op1 divided by op2 into `$a` |
| `$a = op1 ** op2` | Stores the value of op1 to the power of op2 into `$a` |
| `$a = op1 % op2` | Stores the value of op1 modulus op2 into `$a` |
| `op1 == op2` | Returns True if op1 is equal to op2 |
| `op1 != op2` | Returns True if op1 is not equal to op2 |
| `op1 < op2` | Returns True if op1 is less than op2 |
| `op1 > op2` | Returns True if op1 is greater than op2 |
| `op1 <= op2` | Returns True if op1 is less than or equal to op2 |
| `op1 >= op2` | Returns True if op1 is greater than or equal to op2 |

# Strings

Strings are sequences of one or more characters. Usually strings contain alphanumeric characters (such as the numbers from 0 to 9), the upper- and lowercase alphabet, and a handful of punctuation characters. Perl does not distinguish between these characters and nonprintable characters. This means that you can actually use Perl to scan binary files.

Strings are represented in a Perl program in one of two ways: You can enclose a string in double quotation marks or you can enclose a string in single quotation marks. When a string is enclosed in double quotation marks, it behaves in a similar way to strings that are in double quotation marks in C. A backslash can be used in a double quoted string to represent special control characters. A list of the backslash special control characters is shown in Table 28.2.