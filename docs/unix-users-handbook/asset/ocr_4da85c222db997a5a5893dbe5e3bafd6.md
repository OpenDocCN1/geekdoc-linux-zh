following:

```
```text
if(expression) statement [else statement]
while(expression) statement
for(expression;expression;expression) statement
do(var in array) statement
do statement while(expression)
break
continue
[[statement ...]]
expression					# commonly var=expression
print[expression-list] [> expression]
printf format [, expression-list] [> expression]
return [expression]
next					# skip remaining patterns on this input line.
delete array [expression]				# delete an array element.
exit [expression]				# exit immediately; status is expression.
```
```

Statements are terminated by semicolons, newlines or right braces. An empty expression-list stands for $0. String constants are quoted (“”), with the usual C escapes recognized within. Expressions take on string or numeric values as appropriate, and are built using the operators +, -, *, /, %, ^ (exponentiation), and concatenation (indicated by a blank). The operators ++, --, +=, -=, *=, /=, %=, ^=, **=, >, >=, <, <=, ==, !=, and ? are also available in expressions. Variables can be scalars, array elements (denoted x[i]) or fields. Variables are initialized to the null string. Array subscripts can be any string, not necessarily numeric (this allows for a form of associative memory). Multiple subscripts such as [i,j,k] are permitted. The constituents are concatenated, separated by the value of SUBSEP.

The print statement prints its arguments on the standard output (or on a file if >file or >>file is present or on a pipe if |cmd is present), separated by the current output field separator, and terminated by the output record separator. file and cmd can be literal names or parenthesized expressions. Identical string values in different statements denote the same open file. The printf statement formats its expression list according to the format (see printf(3)).

# Built-In Functions

The built-in function close(expr) closes the file or pipe expr opened by a print or printf statement or a call to getline with the same string-valued expr. This function returns zero if successful, otherwise, it returns non-zero.

The customary functions exp, log, sqrt, sin, cos, atan2 are built in. Other built-in functions are:

length([$s])  
Length of its associated argument (in bytes) taken as a string, or of $0 if no argument.

length([[s]])  
Length of its associated argument (in characters) taken as a string, or of $0 if no argument.

rand()  
Returns a random number between zero and one.

srand([expr])  
Sets the seed value for rand, and returns the previous seed value. If no argument is given, the time of day is used as the seed value; otherwise, expr is used.

int(x)  
Truncates to an integer value

substr(s, m[, n])  
Return the at most n-character substring of s that begins at position m, numbering from 1. If