
The printf statement produces output based on a notation similar to the File Format Notation used to describe file formats in this document. Output is produced as specified, with the first expression argument as the string format and subsequent expression arguments as the strings arg1, inclusive, with the following exceptions.

- The format is an actual character string instead of a graphical representation. Therefore, it cannot contain empty character positions. The space character in the format string, in any other context than a flag of a conversion specification, is treated as an ordinary character.

- If the format set contains a \ character and that character appears in the format string, it is treated as an ordinary character that is copied to the output.

- The escape sequences beginning with a backslash character are treated as sequences of ordinary characters that are copied to the output. Note that these same sequences are interpreted literally by awk when they appear in literal strings, but are not treated specially by printf.

- A field or precision can be specified as the * character instead of a digit. In this case, the next argument from the expression is fetched, and its numeric value is taken as the field width or precision.

- The implementation does not precede or follow output from the d or u conversion specifications not specified by the format string.

- The implementation does not precede output from the o conversion specification with leading os not specified by the format string.

- For the c specification: if the argument has a numeric value, the character whose encoding is that value is output. If the value is negative or not the encoding of any character in the character set, the behavior is undefined. If the argument does not have a numeric value, the first character of the string value is output; if the string does not contain any characters, the behavior is undefined.

- For each conversion specification that consumes an argument, the next expression argument is evaluated. With the exception of the c conversion, the value is converted to the appropriate type for the conversion specification.

- If there are insufficient arguments to satisfy all the conversion specifications in the format string, the behavior is undefined.

- If any sequence in the format string begins with a % character but does not form a valid conversion specification, the behavior is unspecified.

Both print and printf can output at least one (LINE_MAX) bytes.

## Functions

The awk language has a variety of built-in functions: arithmetic, string, input/output, and general.

## Arithmetic Functions

The arithmetic functions, except for int, are based on the ISO C standard. The behavior is undefined in cases where the ISO C standard specifies that an error be returned or that although the grammar permits built-in functions to appear with no arguments or parentheses, unless the argument or parentheses are indicated as optional in the following list (by being displayed within the [ ] brackets), use such is undefined.

- atan2(y,x) Return arctangent of y/x
- cos(x) Return cosine of x where x is in radians.
- sin(x) Return sine of x, where x is in radians.
- exp(x) Return the exponential function of x
- log(x) Return the natural logarithm of x
- sqrt(x) Return the square root of x
- int(x) Truncate its argument to an integer. Truncate toward 0 when x > 0.
- rand() Return a random number n, such that 0 < n < 1.

srand([expr]) Set the value for rand to expr, or use the time of day if expr is omitted. Return the previous seed value.

## String Functions

The string functions in this following list are supported. Although the grammar permits built-in functions to appear with no arguments or parentheses, unless the argument or parentheses are indicated as optional in the following list (by being displayed within the [ ] brackets), use such is undefined.

gsub(ere, repl, [in]) Behave like sub (see below), replace all occurrences of the regular expression (like the ed command global substitute) in s0 or in the in argument, when specified.

index(s, t) Return the position, in characters, numbering from 1, in string s where string t occurs, or 0 if it does not occur at all.

length([{s}]) Return the length, in characters, of its argument taken as a string, or of the record, s0, if there is no argument.

match(s, ere) Return the position, in characters, numbering from 1, in string s where the extended regular expression ere occurs, or 0 if it does not occur at all. Set RSTART to the starting position (which is the same as the returned value), 0 if no match is found; set LENGTH to the length of the matched string, -1 if no match is found.

split(s, a[, fs]) Split the string s into array elements a[1], a[2]..., a[n], and return n. Do separation with the extended regular expression fs or the field separator fs if you do not specify fs. Each array element has a string value when created. When any occurrence of the decimal-point character from the current locale is changed to a period character, string assigned to any array element is considered a numeric string; the array element also has the numeric value of the numeric string; the effect of a null string as the value of fs is unspecified.

```
sprintf(fmt, expr, expr, ...)
```
Format the expressions according to the printf format by fmt, and return the resulting string.

```
sub(ere, repl[i,n])
```

Substitute the string repl in place of the first instance of the extended regular expression ere in string and return the number of substitutions. Replace an ampersand (&) in the string with repl from string in that matches the regular expression. For each occurrence of backslash(\) when scanning the string repl from beginning to end, take the next character literally and lose its special meaning (for example, interpret \ as a literal ampersand character). Except for & and \, it is unspecified what the meaning of any such character is. If you specify in and it is not an value, the behavior is undefined. If you omit it, substitute the current record (0).

```
substr(s, m[,n])
```
Return at most the n-character substring of s that begins at position m numbering from 1. If n is missing, limit the length of the substring by the length of the string s.

```
tolower(s)
```
Return a string based on the string s. In the returned string, replace each character in s that is an uppercase letter specified to have a tolower mapping by the LC_TYPE category of the current locale with the lowercase letter specified by the mapping. Other characters in s are unchanged in the returned string.

```
toupper(s)
```
Return a string based on the string s. In the returned string, replace each character in s that is a lowercase letter specified to have a toupper mapping by the LC_TYPE category with the uppercase letter specified by the mapping. Other characters in s are unchanged in the returned string.

All of the preceding functions that take ERE as a parameter expect a pattern or a string-valued expression that is a regular expression defined below.

## Input/Output and General Functions

The input/output and general functions are listed below.

```
close(expression)
```
Close the file or pipe opened by a print or printf statement or a call to getline with the same string-valued expression. If the close was successful, return 0; otherwise, return non-zero.

```
expression | getline [var]
```
Read a record of input from a stream piped from the output of a command. If no stream is currently open, create the stream with the value of expression as its command name. The stream created is equivalent to one created by a call to the popen function with the value of expression as the command argument and a value of r as the argument. As long as the stream remains open, subsequent calls in which expression evaluates to the same string value read subsequent records from the file. The file remains open until the close function is called with an expression that evaluates to the same string value. If var is missing, $0 and NF are set; otherwise, var is set.

The getline operator can form ambiguous constructs when there are not in parentheses (including concatenate) to the left of the | (to the beginning of the expression containing getline). In the context of the $ | behaves as if it had a lower precedence than $. The result of evaluating other operators is unspecified, and all uses of portable applications must be put in parentheses.

getline Set $0 to the next input record from the current input file. This form of getline sets the NF, NR, and FNR variables.

getline var Set var to the next input record from the current input file. This form of getline sets the FNR and NR variables.

getline [var] < expression Read the record of input from a named file. The expression is evaluated to produce a string that is used as a full path name. If the file of that name is not currently open, open it. As long as the stream remains open, subsequent calls in which expression evaluates to the same string value read subsequent records from the file. The file remains open until the close function is called with an expression that evaluates to the same string value. $0 and NF are set; otherwise, var is set.

```
system(expression)
```
Execute the command given by expression in a manner equivalent to the system (3S), and return the exit status of the command.

All forms of getline return 1 for successful input, 0 for end-of-file, and -1 for error.

Where strings are used as the name of a file or pipeline, the strings must be textually identical. The terminology "same string value" implies "equivalent strings", even those that differ only by space characters, represent different files.
