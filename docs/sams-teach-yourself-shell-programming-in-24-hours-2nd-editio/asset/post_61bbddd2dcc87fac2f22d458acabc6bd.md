
To embed integer calculations within a command, you can use the following syntax:

```
$((integer_expression))
```

## Integer Expression Operators

The integer operators are used to perform simple arithmetic operations on integer values.

The following list (order from highest to lowest operator precedence) describes the integer operators supported in ksh, bash and zsh. The logical operators described in this list return 1 for true and 0 for false.

- `-` unary minus (negates the following value)
- `!` logical NOT, binary one's complement
- `* / %` multiply, divide, modulus (remainder operation)
- `+ -` add, subtract
- `>> <<` right, left shift, for example: `$((32 >> 2))` gives 8 (right shift 32 by 2 bits is the same as division by 4)
- `<= >=` less than or equal to, greater than or equal to
- `> <` greater than, less than
- `== !=` equal to, not equal to
- `&` bitwise AND operation, for example: `$((5 & 3))` converts 5 to binary 101 and 3 to binary 011 and ANDs the bits to give 1 as the result
- `^` bitwise exclusive OR operation
- `|` bitwise regular OR operation
- `&&` logical AND
- `||` logical OR
- `*= /= %=` C programming type assignment, for example, `$((A *= 2))` means multiply variable A by 2, save result in A, and substitute result
- `+= -= ...` more C programming type assignments
- `>>= <<=` more C programming type assignments using shift right, shift left
- `&= ^= |=` more C programming type assignments using AND, exclusive OR, and regular OR

![](img/3def70414996f811615f713b2077a154_440_0.png)

## Parameters and Variables

This section describes parameters and variables.

### User-Defined Variables

Any variable defined by a programmer is a user defined variable. User-defined variable names

- Must start with letters
- Can contain only letters or digits
- Are often in capital letters to differentiate them from UNIX commands

Variables are assigned values using the assignment operator, =, as follows:

```
VAR=value
```

Here, VAR is the name of the variable and value is the value you want to assign to it.

Variables are unset using the unset command as follows:

```
unset var1 ... varN
```

Here var1 ... varN are the names of the variables to unset.

### Variable Substitution

The value stored in a variable can be accessed using the $ operator as follows:

```
$VAR
```

Here VAR is the name of the variable whose value you want to access. Other forms of variable substitution include the following:

${var} substitutes the contents of var, which can be a variable name or digit indicating a positional parameter

${var:-word} substitutes the contents of var but if it is empty or undefined, it substitutes word, which might contain unquoted spaces

${var:=word} substitutes the contents of var but if it is empty or undefined, it sets var equal to word and substitutes word

${var:?word} substitutes the contents of var, but if it is empty or undefined, aborts the script and gives the message as a final error. Message might contain unquoted spaces.

${var:+word} if var is not empty, it substitutes word; otherwise it substitutes nothing

## Array Variables (ksh, bash, and zsh Only)

Arrays provide a method for grouping variables using a single variable name coupled with an index. The index must always be a positive integer. In ksh the maximum value for index is 1024. No such limit exists in bash or zsh.

In ksh and zsh array variables are initialized using the set command as follows:

```
set -A ARRAY val1 ... valN
```

In bash, array variables are initialized as follows:

```
ARRAY=(val1 ... valN)
```

In either case ARRAY is the name of the array and val1 ... valN are the values for the first N elements in the array.

Arrays are not available in the Bourne shell and 1.x and earlier versions of bash.

- `ARRAY[index]=value` sets the value of the element denoted by index in ARRAY to value
- `${ARRAY[index]}` substitutes the value of the element index in ARRAY.
- `${ARRAY[*]}` substitutes all elements in ARRAY
- `${ARRAY[@]}` substitutes all array elements in ARRAY and treats each element as if individually double-quoted

## Special Variables

The following are special variables that are created and modified by the shell itself. These variables cannot be changed by scripts.

| Variable | Description |
|---|---|
| $0 | name of the command or script being executed |
| $n | positional parameters—that is, arguments given on the command line numbered 1 through 9 |
| $# | number of positional parameters given on command line |
| $* | a list of all the command-line arguments |
| $@ | a list of all command-line arguments individually double-quoted |
| $? | The numeric exit status (that is, return code) of last command executed |
| $$ | PID (process ID) number of current shell |
| $! | PID (process ID) number of last background command |

## Shell Variables

The following variables are used by the shell, but can be modified by scripts.

**CDPATH** contains a colon-separated list of directories to facilitate the cd command.

**HOME** is your home directory.

**IFS** contains internal field separator characters.

**OPTARG** is the last end line arg processed by getopts (Korn/Bash).

**OPTIND** is the index of the last end line arg processed by getopts (Korn/Bash).

**PATH** contains a colon-separated list of directories to search for commands that are given without any slash.

**PS1** is the primary shell prompt string.

**PS2** is the secondary shell prompt string for continuation lines.

**PWD** returns the current directory.

**RANDOM** returns a different random number (from 0 to 32,767) each time it is invoked (ksh, bash, and zsh only).

**REPLY** is the last input line from read via the select command (ksh, bash, and zsh only).

**SECONDS** returns the number of seconds since shell invocation (ksh, bash, and zsh only).

**SHLVL** returns the number of shells currently nested.

**UID** is the numeric user ID number.

## Input/Output

This section discusses I/O. Table A.1 describes the standard UNIX file descriptors, whereas other sections describe input and output redirections and "here" documents.

TABLE A.1 Summary of Standard UNIX I/O

| Abbreviation | I/O description | File Descriptor |
|---|---|---|
| STDIN | Standard input | 0 |
| STDOUT | Standard output | 1 |
| STDERR | Standard error | 2 |

### Input and Output Redirection

Input and output redirection can be performed as follows:

- `cmd > file` save STDOUT from UNIX command in file
- `cmd 1> file` same as above
- `cmd >> file` append STDOUT from UNIX command to file
- `cmd 1>> file` same as above
- `cmd 2> file` save STDERR from UNIX command in file
- `cmd 2>> file` append STDERR from UNIX command to file
- `cmd < file` provide STDIN to UNIX command from file instead of keyboard
- `cmd 0< file` same as above
- `cmd1 | cmd2` pipe STDOUT of cmd1 as STDIN to cmd2
- `cmd | tee file` save STDOUT of UNIX command in file but also pass same text as STDOUT
- `exec n> file` redirect output of file descriptor n to (overwrite) file. This applies to subsequent UNIX commands.
- `exec n>> file` same as above but append to file instead of overwriting
- `cmd 2>&1` redirect STDERR from UNIX command to wherever STDOUT is currently going
- `cmd 1>&2` redirect STDOUT as STDERR. This should be done when echo displays an error message.
- `cmd n>&m` redirect file descriptor n to wherever file descriptor m is currently going. This is a generalization of the previous examples.
- `exec n>&-` close file descriptor n

### Here Document

Here documents provide STDIN to UNIX commands from lines that follow until delimiter is found at the start of line:

```
cmd << delimiter
line1
lineN
delimiter
```

![](img/3def70414996f811615f713b2077a154_444_0.png)

## Pattern Matching and Regular Expressions

This section describes the meta-characters and rules for filename expansion, pattern matching for the case statement, and regular expressions.

### Filename Expansion and Pattern Matching

The rules for filename expansion are as follows:

- Any word on the command line that contains a meta-character is expanded to a list of files that match the pattern word.
- If no filename matches are found, the pattern word is not substituted.
- Meta-characters cannot match a leading period or a slash.

The filename expansion meta-characters are

| Symbol | Meaning |
|---|---|
| * | matches 0 or more of any character |
| ? | matches exactly 1 of any character |
| [list] | matches exactly 1 of any character in list |
| [^list] | matches exactly 1 of any character not in list |

### Limited Regular Expression Wildcards

All regular expression patterns can include these wildcards:

| Symbol | Meaning |
|---|---|
| ^pattern | only matches if pattern is at the start of a line |
| pattern$ | only matches if pattern is at the end of a line |
| . | matches exactly 1 of any character |
| [list] | matches exactly 1 of any character in list |
| [^list] | matches exactly 1 of any character not in list |
| * | matches 0 or more repetitions of the previous element (char or expression) |
| .* | matches 0 or more of any characters |

### Extended Regular Expression Wildcards

These are additional regular expression wildcards that are only supported in some commands:

| Symbol | Meaning |
|---|---|
| {n} | matches n repetitions of the previous element |
| {n,} | matches n or more repetitions of the previous element |
