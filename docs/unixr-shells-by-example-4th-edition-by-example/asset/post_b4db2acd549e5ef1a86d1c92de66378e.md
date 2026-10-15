
## Table 6.11 Assignment Operators

| Operator | Meaning | Equivalence |
|---|---|---|
| = | a = 5 | a = 5 |
| += | a = a + 5 | a += 5 |
| -= | a = a - 5 | a -= 5 |
| *= | a = a * 5 | a *= 5 |
| /= | a = a / 5 | a /= 5 |
| %= | a = a % 5 | a %= 5 |
| ^= | a = a ^ 5 | a ^= 5 |

The simplest assignment takes the result of an expression and assigns it to a variable.

## FORMAT

```
variable = expression
```

## EXAMPLE 6.86

```
% nawk '$1 ~ /Tom/ { wage = $2 * $3; print wage }' filename
```

## EXPLANATION

Awk will scan the first field for Tom and when there is a match, it will multiply the value of the second field by the value of the third field and assign the result to the user-defined variable wage. Because the multiplication operation is arithmetic, awk assigns wage an initial value of zero. (The % is the shell prompt and filename is an input file.)

## Increment and Decrement Operators.

To add one to an operand, the increment operator is used. The expression x++ is equivalent to x = x + 1. Similarly, the decrement operator subtracts one from its operand. The expression x-- is equivalent to x = x - 1. This notation is useful in looping operations when you simply want to increment or decrement a counter. You can use the increment and decrement operators either preceding the operator, as in ++x, or after the operator, as in x++. If these expressions are used in assignment statements, their placement will make a difference in the result of the operation.

```
{x = 1; y = x++ ; print x, y}
```

The ++ here is called a post-increment operator: y is assigned the value of 1, and then x is increased by 1, so that when all is said and done, y will equal 1, and x will equal 2.

```
{x = 1; y = ++x; print x, y}
```

The ++ here is called a pre-increment operator; x is incremented first, and the value of two is assigned to y, so that when this statement is finished, y will equal 2, and x will equal 2.

## User-Defined Variables at the Command Line.

A variable can be assigned a value at the command line and passed into an awk script. For more on processing arguments and ARGV, see "Processing Command Arguments (nawk)" on page 239.

## EXAMPLE 6.87

```
nawk -F: -f awk script   month=4 year=2004 filename
```

## EXPLANATION

The user-defined variables month and year are assigned the values 4 and 2004, respectively. In the awk script, these variables may be used as though they were created in the script. Note: If filename precedes the arguments, the variables will not be available in the BEGIN statements. (See "BEGIN Patterns" on page 208.)

## The -v Option (nawk).

The -v option provided by nawk allows command-line arguments to be processed within a BEGIN statement. For each argument passed at the command line, there must be a -v option preceding it.

## Field Variables.

Field variables can be used like user-defined variables, except they reference fields. New fields can be created by assignment. A field value that is referenced and has no value will be assigned the null string. If a field value is changed, the $0 variable is recomputed using the current value of OFS as a field separator. The number of fields allowed is usually limited to 100.

## EXAMPLE 6.88

```
% nawk '{ $5 = 1000 * $3 / $2; print $ }' filename
```

## EXPLANATION

If $5 does not exist, nawk will create it and assign the result of the expression 1000 * $3 / $2 to the fifth field ($5). If the fifth field exists, the result will be assigned to it, overwriting what is there.

## EXAMPLE 6.89

```
% nawk '$4 == "CA" { $4 = "California"; print}' filename
```

## EXPLANATION

If the fourth field ($4) is equal to the string CA, awk will reassign the fourth field to California. The double quotes are essential. Without them, the strings become user-defined variables with an initial value of null.

Built-In Variables. Built-in variables have uppercase names. They can be used in expressions and can be reset. See Table 6.12 for a list of built-in variables.

## Table 6.12 Built-In Variables

| Variable Name | Contents |
|---|---|
| ARGC | Number of command-line argument |
| ARGIND | Index in ARGV of the current file being processed from the command line (gawk only) |
| ARGV | Array of command-line arguments |
| CONVMT | Conversion format for numbers, % .6g, by default (gawk only) |
| ENVIRON | An array containing the values of the current environment variables passed in from the shell |
| ERRNO | Contains a string describing a system error occurring from redirection when reading from the getline function or when using the close function (gawk only) |
| FIELDWIDTHS | A whitespace-separated list of fieldwidths used instead of FS when splitting records of fixed fieldwidth (gawk only) |
| FILENAME | Name of current input file |
| FNR | Record number in current file |
| FS | The input field separator, by default a space |
| IGNORECASE | Turns off case sensitivity in regular expressions and string operations (gawk only) |
| NF | Number of fields in current record |
| NR | Number of records so far |
| OFMT | Output format for numbers |
| OFS | Output field separator |
| ORS | Output record separator |
| RLENGTH | Length of string matched by match function |
| RS | Input record separator |
