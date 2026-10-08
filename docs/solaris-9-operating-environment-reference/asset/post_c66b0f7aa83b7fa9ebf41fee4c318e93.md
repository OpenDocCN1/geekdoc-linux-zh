
# nawk

| Syntax | Name | Type of Result | Associativity |
| --- | --- | --- | --- |
| expr <= expr | Less than or equal to | Numeric | None |
| expr != expr | Not equal to | Numeric | None |
| expr == expr | Equal to | Numeric | None |
| expr > expr | Greater than | Numeric | None |
| expr >= expr | Greater or equal to | Numeric | None |
| expr ~ expr | ERE match | Numeric | None |
| expr !~ expr | ERE nonnegative | Numeric | None |
| expr in array | Array membership | Numeric | Left |
| index ( ) in array | Multidimension array membership | Numeric | Left |
| expr && expr | Logical AND | Numeric | Left |
| expr || expr | Logical OR | Numeric | Left |
| expr1 ? expr2 : expr3 | Conditional expression | Type of selected | Right |
| value ^= expr | Exponentiation assignment | Numeric | Right |
| value %= expr | Modulus assignment | Numeric | Right |
| value *= expr | Multiplication assignment | Numeric | Right |
| value /= expr | Division assignment | Numeric | Right |
| value += expr | Addition assignment | Numeric | Right |
| value -= expr | Subtraction assignment | Numeric | Right |
| value = expr | Assignment | Type of expr | Right |

Each expression has a string value, a numeric value, or both. Except as stated for specific contexts, the value of an expression is implicitly converted to the type needed for the context in which it is used. A string value is converted to a numeric value by the equivalent of the following calls:

```
setlocale(LC_NUMERIC, ""); numeric_value = atof(string_value);
```

A numeric value that is exactly equal to the value of an integer is converted to a string by the string of a call to the sprintf function, with the string %d as the Lmt argument and the numeric value being converted as the first and only expr argument. Any other numeric value is converted to a string by the equivalent of a call to the sprintf function, with the value of the variable conv as the Lmt argument and the numeric value being converted as the first and only expr argument.

A string value * is considered a numeric string in the following cases:

- Any leading and trailing blank characters are ignored.
- If the first unignored character is a + or - , it is ignored.
- If the remaining unignored characters would be lexically recognized as a NUMBER token, the string is considered a numeric string.
- If a character - is ignored in the above steps, the negative of the numeric value of the recognized NUMBER token is the numeric value of the numeric string. Whether a string is a numeric string is relevant only in contexts where that term is used in this section.
- When an expression is used in a Boolean context, if it has a numeric value, a value of 0 is treated as false and any other value is treated as true. Otherwise, a string value of null string is treated as false, and any other value is treated as true. A Boolean context is one of the following:
- The first subexpression of a conditional expression.
- An expression operated by logical NOT, logical AND, and logical OR.
- The second expression of a for statement.
- The expression of an if statement.
- The expression of the while clause in either a while or do...while statement.
- An expression used as a pattern (as in Overall Program Structure).

The nawk language supplies arrays that are used for storing numbers or strings. Arrays need not be declared. They are initially empty and their sizes change dynamically. The subscript or element identifiers are strings, providing a type of associative array capacity. You can use an array name followed by a subscript within square brackets and as an expression, as described in the grammar. Unsubscribed array names are used only in the following contexts:

- A parameter in a function definition or call.
- The NAME token following any one of the keyword in.

A valid index consists of one or more comma-separated expressions, similar to the way that multidimensional arrays are indexed in some programming languages. Because nawk arrays are really one dimensional, nawk converts such a comma-separated list to a single string by concatenating the string value of the separate expressions, each separated from the other by the value of the SUBSEP variable. Thus, the two index operations are equivalent.

```
var[expr1,expr2,...exprn]
var[expr1 SUBSEP expr2 SUBSEP... exprn]
```

You must enclose in parentheses a multidimensional index used with the in operator. The in operator tests for the existence of a particular array element, does not create the element if it does not exist. Any other reference to a nonexistent array element automatically creates it.

# Variables and Special Variables

You can use variables in a nawk by referencing them. With the exception of function parameters, variables are not explicitly declared. Uninitialized scalar variables and array elements both have a numeric value of 0 and a string value of the empty string.

Field variables are designated by $ followed by a number or numerical expression.
The effect of the field number expression evaluating to anything other than a integer is unspecified. You do not need to convert uninitialized variables or string values to numeric values in this context. Create new field variables by assigning a value to them. References to nonexistent fields (that is, fields after $NF) produce the null string. However, assigning to a nonexistent field (for example, $(NF+2) = 5) increases the value of $NF, creating any intervening fields with null string as its values, and computes the value of $0 with the fields separated by the OFS. Each field variable has a string value created when. When the decimal-point character from the current locale is changed to a period character, the string is considered a numeric string, the field variable also has the numeric value of the numeric string.

awk sets the following special variables:

- ARGC: The number of elements in the ARGV array.
- ARGV: an array of command-line arguments excluding options and the program argument, numbered from 0 to ARGC-1.

You can modify or add the arguments to ARGV. You can alter each input field ends, nauk treats the next non-null element of ARGC, up to the current value of ARGC-1, inclusive as the name of the next input field. Setting an element of ARGV to null means that it is not treated as an input file. The name- indicates the standard input. If an argument matches the format of an assignment operand, this argument is treated as an assignment instead of a file.

- OFMT: The printf format for converting numbers to strings (except for output statements, where OFMT is used); %.6g by default.
- ENVIRON: an array representing the value of the environment. The indices of the array are strings consisting of the names of the environment.
- FILENAME: A path name of the current input. Inside a BEGIN action, the value is undefined. Inside an END action, the value is the name of the last file.
- FNR: The ordinal number of the current record. Inside a BEGIN action, the value is 0. Inside an END action, the value is the number of the last record.
- FS: Input field separator expression; by default, a space character.
- NF: The number of fields in the current record. Inside a BEGIN action, the value is undefined unless a getline function without var argument is executed. Inside an END action, NF retains the value it had for the last record.
- RS: The first character of the string value of RS is the input record separator; by default, a newline. If RS contains more than one character, the results are unspecified. If RS is null, records are separated by sequences of one or more blank lines; leading or trailing blank lines do not produce empty records at the beginning or end of input, and the field separator is always newline.
- OFS: The print output field separator; by default, a space character.
- ORS: The print output record separator; by default, a newline character.
- LEN: The length of the string matched by the match function.
- START: The starting position of the string matched by the match function, numbering from 1. This value is always equal to the return value of the match function.
- SUBSEP: The subscript separator string for multidimensional arrays; the default value is 1.

# Regular Expressions
Theawk command uses the extended regular expression (see regex(5)) except that it allows the use of C-language conventions to escape special characters within the EREs, namely, \\, \a, \b, \f, \n, \t, and those specified in the following table. These escape sequences are recognized both inside and outside bracket expressions.

> Note — You do not need to separate records with newline characters, and string constants can contain newline characters, so even the \n sequence is valid in awk EREs. Using a slash character within the regular expression requires escaping as shown in the table below.

| Escape | Description | Meaning |
|---|---|---|
| | Backslash quotation mark. | Quotation mark character. |
