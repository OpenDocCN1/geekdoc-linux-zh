
# File-Name Generation

Following substitution, each command word is scanned for the characters *, 2, and [ unless you specify the -f option. If one of these characters appear, the word is regarded as a pattern. The word is replaced with lexicographically sorted file names that match the pattern. If no file name matches the pattern is found, the word is left unchanged. When a pattern is used for file-name generation, the character . at the start of a file name or immediately following /, as well as the character / itself, must be explicitly matched. A file name beginning with a dot is not matched with a pattern with the dot inside parentheses; that is, .(.*) would locate a file named .restore.

In instances of pattern matching, the / and & are not treated specially.

- Match any null string.
- Match any single character.
- Match any one of the enclosed characters. A pair of characters separated by - matches any character literally between the pair, inclusive. If the first character following the opening square bracket ([ is an exclamation mark (!), then any character not enclosed is matched. You can include a dash (-) in the character set by putting it as the first or last character.

A pattern-list is a list of one or more patterns separated from each other with a |. You can form composite patterns with one or more of the following.

- ?(pattern-list)
Optionally match any one of the given patterns.
- *( pattern-list)
Match zero or more occurrences of the given patterns.
- +(pattern-list)
Match one or more occurrences of the given patterns.
- @(pattern-list)
Match exactly one of the given patterns.
- !(pattern-list)
Match anything except one of the given patterns.

# Quoting (Escaping) Characters

Each of the metacharacters has a special meaning to the shell. To remove the normal meaning, you can quote it. (Note that in other contexts, term escape is used to describe this action.) You can quote a single character (that is, make it stand for itself) by preceding it with a backslash. The pair \newline is removed.
To quote a string of characters, you can enclose them in quotes.

- * All characters enclosed between a pair of single quote marks ('') are quoted. A single quote cannot appear within single quotes.
- Inside double-quotes (""), parameter and command substitution occurs, and \ quotes the characters \', \", and \$ and $ is identical when not quoted or used as a parameter assignment value or as a name.

# ksh, rksh

However, when used as a command argument, $ is equivalent to $1d2d3... where d is the first character of the IFS variable, whereas $0 is equivalent to $12...

- - Inside grave quote marks (``), quotes the characters \ and s. If the grave quotes occurs within double quotes, then \ also quotes the character *.

You can remove the special meaning of reserved words or aliases by quoting any character of the reserved word. You cannot alter the recognition of function names or special commands by quoting them.

# Arithmetic Evaluation

The let command provides the capability of performing integer arithmetic.
Evaluations are performed using long arithmetic. Constants are of the form [$base] n where base is a decimal number between 2 and 36 representing the arithmetic base and n is a number in that base. If you omit base, then base 10 is used. An arithmetic expression uses the same syntax, precedence, and associativity of expression as the C language. All the integral operators, other than +, -, ?, and are supported. You can reference variables by name within an arithmetic expression without using the parameter substitution. When you refer a variable, its value is evaluated as an arithmetic expression.

You can specify an integer representation of a variable with the -i option of typeset command. Arithmetic evaluation is performed on the value of each assignment to a variable with the -attribute. If you do not specify an arithmetic base, the first assignment to the variable determines the arithmetic base. This base is used when parameter substitution occurs. Many of the arithmetic operators require quoting, an alternative form of the let command is provided. For any command that begins with a ((, all the characters until a matching )) are treated as a quoted expression. More precisely, (()) is equivalent to let *.

# Conditional Expressions

Use conditional expressions with the [[ compound command to test attributes of and to compare strings.

- Word splitting and file-name generation are not performed on the words between [ and ]]. Each expression can be constructed from one or more of the following unary or binary expressions.
- a
- b
- c
- d
- e
- f
- g
- k
- n
- o
- p
- r
- s
- t
- u
- w
- x
- z
- A
- G
- L
- O
- S
- X
- nt
- ot
- ef
- binary expressions:
- (
- ( )
- !
- &&
- ||
- =
- !=
- <
- >
- <=
- -eq
- -ne
- -lt
- -gt
- -le
- -ge

In each of the above expressions, if file of the form /dev/fd/n, where n is an integer, the test is applied to the open file whose descriptor number is n. You can construct a compound expression from these using any of the following, listed in decreasing order of precedence.

- (expression)
true if expression is true. To group expressions.
- ! expression
true if expression is false.
- expression1 && expression2
true if expression1 and expression2 are both true.
- expression1 || expression2
true if either expression1 or expression2 is true.

# Environment Variables

The (see environ(5)) is a list of name-value pairs that is passed to an executed program in the shell as a normal argument list. The names must be identifiers, and the values are character strings. The shell interacts with the environment in several ways. On invocation, the shell scans the environment and creates a variable for each name found, giving the corresponding value and marking it. Export commands inherit the environment. If the user modifies the values of these variables creates new ones using the export or typeset -x commands, they become part of the environment. The environment seen by any executed command is thus composed of any name-value pairs originally inherited by the shell, whose values are modified by the current shell, plus any additions that must be noted in export -x commands.

You can augment the environment for any simple command or function by prefixing it with one or more variable assignments. A variable assignment argument is a word of the form identifier=value. Thus:

```
TERM=450 cmd args
```
