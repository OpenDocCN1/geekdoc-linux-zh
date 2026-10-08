+   SUBSEP The subscript separator string for multi- dimensional arrays; the default value is " 34" ARGC The number of elements in the ARGV array. ARGV An array of command line arguments, excluding options and the program argument numbered from zero to ARGC-1. The arguments in ARGV can be modified or added to; ARGC can be altered. As each input file ends, awk will treat the next non-null element of ARGV, up to the current value of ARGC-1, inclusive, as the name of the next input file. Thus, setting an element of ARGV to null means that it will not be treated as an input file. The name - indicates the standard input. If an argument matches the format of an assignment operand, this argument will be treated as an assignment rather than a file argument. ENVIRON Array of environment variables; subscripts are names. For example, if environment variable V=thing, ENVIRON["V"] produces thing. RSTART The starting position of the string matched by the match function, numbering from 1. This is always equivalent to the return value of the match function. RLENGTH The length of the string matched by the match function.

Functions can be defined (at the position of a pattern-action statement) as follows:

```
function foo(a, b, c) { ...; return x }
```

Parameters are passed by value if scalar, and by reference if array name. Functions can be called recursively. Parameters are local to the function; all other variables are global.

Note that if pattern-action statements are used in an HP-UX command line as an argument to the awk command, the pattern-action statement must be enclosed in single quotes to protect it from the shell. For example, to print lines longer than 72 characters, the pattern-action statement as used in a script (-f profile command form) is:

```
length > 72
```

The same pattern action statement used as an argument to the awk command is quoted in this manner:

```
awk 'length > 72'
```

# EXTERNAL INFLUENCES

# Environment Variables

+   LANG Provides a default value for the internationalization variables that are unset or null. If LANG is unset or null, the default value of "C" (see lang(5)) is used. If any of the internationalization variables contains an invalid setting, awk will behave as if all internationalization variables are set to "C". See environ(5).