
# paste - Merge lines of files.

Options

- -d list Use list as the delimiter between columns. You can use special escape sequences for list such as \n for newline and \t for tab.

![](img/75f39fc91296b889c0653851accdfd46_663_0.png)
![](img/75f39fc91296b889c0653851accdfd46_663_1.png)

# join - Combine two presorted files that have a common key field.

Options

- -a n Produce the normal output and also generate a line for each line that can't be joined in 1 or 2.
- -e string Replace empty fields in output with string.
- -t char Use char as the field separator.

# tr

![](img/75f39fc91296b889c0653851accdfd46_663_2.png)

**tr** translates characters. **tr** is ideal for such tasks as changing case. For instance, what if you want to translate all lowercase characters to upper case? The following example shows listing files that have the suffix "zip" and then translates these files into uppercase:

![](img/75f39fc91296b889c0653851accdfd46_663_3.png)

```
$ ls -al *.zip
file1.zip
file2.zip
file3.zip
file4.zip
file5.zip
file6.zip
file7.zip
$ ls -al *.zip | tr "[:lower:]" "[:upper:]"
FILE1.ZIP
FILE2.ZIP
FILE3.ZIP
FILE4.ZIP
FILE5.ZIP
FILE6.ZIP
FILE7.ZIP
$
```

We use brackets in this case, because we are translating a class of characters.

The following is a summary of the **tr** command, with some of the more commonly used options.

![](img/75f39fc91296b889c0653851accdfd46_664_0.png)

# **tr** - Translate characters.

# Options

- -A Translate on a byte-by-byte basis.
- -d Delete all occurrences of characters specified.
- [:class:] Translate from one character class to another such as from lowercase class to uppercase class, as shown in the example.

# Manual Pages of Some Commands Used in Chapter 10

The following are the HP-UX manual pages for many of the commands used in the chapter. Commands often differ among UNIX variants, so you may find differences in the options or other areas for some commands; however, the following manual pages serve as an excellent reference.

![](img/75f39fc91296b889c0653851accdfd46_666_0.png)

# **awk - Pattern-processing language.**

## awk(1)

## NAME

awk - pattern-directed scanning and processing language

## SYNOPSIS

```
awk [-Ff s] [-v var=value] [program | -f progfile ...] [file ...]
```

## DESCRIPTION

awk scans each input file for lines that match any of a set of patterns specified literally in program or in one or more files specified as *-f progfile*. With each pattern there can be an associated action that is to be performed when a line in a file matches the pattern. Each line is matched against the pattern portion of every pattern-action statement, and the associated action is performed for each matched pattern. The file name *- * means the standard input. Any file of the form *var=value* is treated as an assignment, not a filename. An assignment is evaluated at the time it would have been opened if it were a filename, unless the *-v* option is used.

An input line is made up of fields separated by white space, or by regular expression *FS*. The fields are denoted *$1, $2, ..., $0* refers to the entire line.

## Options

awk recognizes the following options and arguments:

- -F fs     Specify regular expression used to separate fields. The default is to recognize space and tab characters, and to discard leading spaces and tabs. If the *-F* option is used, leading input field separators are no longer discarded.
- -f progfile Specify an awk program file. Up to 100 program files can be specified. The pattern-action statements in these files are executed in the same order as the files were specified.
- -v var=value Cause *var=value* assignment to occur before the BEGIN action (if it exists) is executed.

## Statements

A pattern-action statement has the form:

```
pattern { action }
```

A missing { action } means print the line; a missing pattern always matches. Pattern-action statements are separated by new-lines or semicolons.

An action is a sequence of statements. A statement can be one of the following:

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

Statements are terminated by semicolons, newlines or right braces. An empty expression-list stands for $0. String constants are quoted (“”), with the usual C escapes recognized within. Expressions take on string or numeric values as appropriate, and are built using the operators +, -, *, /, %, ^ (exponentiation), and concatenation (indicated by a blank). The operators ++, --, +=, -=, *=, /=, %=, ^=, **=, >, >=, <, <=, ==, !=, and ? are also available in expressions. Variables can be scalars, array elements (denoted x[i]) or fields. Variables are initialized to the null string. Array subscripts can be any string, not necessarily numeric (this allows for a form of associative memory). Multiple subscripts such as [i,j,k] are permitted. The constituents are concatenated, separated by the value of SUBSEP.

The print statement prints its arguments on the standard output (or on a file if >file or >>file is present or on a pipe if |cmd is present), separated by the current output field separator, and terminated by the output record separator. file and cmd can be literal names or parenthesized expressions. Identical string values in different statements denote the same open file. The printf statement formats its expression list according to the format (see printf(3)).

## Built-In Functions

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
Return the at most n-character substring of s that begins at position m, numbering from 1. If n is omitted, the substring is limited by the length of string s.

index(s, t) | Return the position, in characters, numbering from 1, in string s where string t first occurs, or zero if it does not occur at all.

match(s, ere) | Return the position, in characters, numbering from 1, in string s where the extended regular expression ere occurs, or 0 if it does not. The variables RSTART and RLENGTH are set to the position and length of the matched string.

split(s, a[, fs]) | Splits the string s into array elements a[1], a[2], ..., a[n], and returns n. The separation is done with the regular expression fs, or with the field separator FS if fs is not given.

sub(ere, repl [, in]) | Substitutes repl for the first occurrence of the extended regular expression ere in the string in. If in is not given, $0 is used.

gsub | Same as sub except that all occurrences of the regular expression are replaced; sub and gsub return the number of replacements.

sprintf(fmt, expr, ...) | String resulting from formatting expr ... according to the printf(3S) format fmt

system(cmd) | Executes cmd and returns its exit status

toupper(s) | Converts the argument string s to uppercase and returns the result.

tolower(s) | Converts the argument string s to lowercase and returns the result.

The built-in function getline sets $0 to the next input record from the current input file; getline < file sets $0 to the next record from file. getline x sets variable x instead. Finally, cmd | getline pipes the output of cmd into getline; each call of getline returns the next line of output from cmd. In all cases, getline returns 1 for a successful input, 0 for end of file, and -1 for an error.

## Patterns

Patterns are arbitrary Boolean combinations (with ! || &&) of regular expressions and relational expressions. awk supports Extended Regular Expressions as described in regex(5). Isolated regular expressions in a pattern apply to the entire line. Regular expressions can also occur in relational expressions, using the operators = and !. /re/ is a constant regular expression; any string (constant or variable) can be used as a regular expression, except in the position of an isolated regular expression in a pattern.

A pattern can consist of two patterns separated by a comma; in this case, the action is performed for all lines from an occurrence of the first pattern though an occurrence of the second.

A relational expression is one of the following:

- expression matchop regular-expression
- expression rel op expression
- expression in array-name
- (expr,expr,...) in array-name
