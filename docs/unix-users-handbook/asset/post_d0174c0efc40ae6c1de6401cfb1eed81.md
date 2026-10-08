
and IFS, HOME, SHELL, ENV, and MAIL are never set automatically by the shell (although HOME, SHELL, and MAIL are set by login(1)).

## Blank Interpretation

After parameter and command substitution, the results of substitution are scanned for field separator characters (found in IFS), and split into distinct arguments where such characters are found. ksh retains explicit null arguments (`""` or `''`) but removes implicit null arguments (those resulting from parameters that have no values).

## File Name Generation

Following substitution, each command word is processed as a pattern for file name expansion unless the -f option has been set. The form of the patterns is the Pattern Matching Notation defined by regexp(5). The word is replaced with sorted file names matching the pattern. If no file name is found that matches the pattern, the word is left unchanged.

In addition to the notation described in regexp(5), ksh recognizes composite patterns made up of one or more pattern lists separated from each other with a `|`. Composite patterns can be formed with one or more of the following:

- `*(pattern-list)` - Optionally matches any one of the given patterns.
- `*(pattern-list)` - Matches zero or more occurrences of the given patterns.
- `+(pattern-list)` - Matches one or more occurrences of the given patterns.
- `@(pattern-list)` - Matches exactly one of the given patterns.
- `!(pattern-list)` - Matches anything, except one of the given patterns.

## Quoting

Each of the metacharacters listed above (See Definitions above) has a special meaning to the shell and causes termination of a word unless quoted. A character can be quoted (i.e., made to stand for itself) by preceding it with a `\`. The pair `\` newline is ignored. All characters enclosed between a pair of single quote marks (`'`), are quoted. A single quote cannot appear within single quotes. Inside double quote marks (`"`), parameter and command substitution occurs and `\` quotes the characters `\`, `'`, `"`, and `$`. `$` and `$\` have identical meanings when not quoted or when used as a parameter assignment value or as a file name. However, when used as a command argument, `"*$\`" is equivalent to `"$1$2...`, where d is the first character of the IFS parameter, whereas `"$$"` is equivalent to `"$1" "$2" ...`. Inside back single quote (accent grave) marks (`` ` ``) `\` quotes the characters `\`, `'`, and `$`. If the back single quotes occur within double quotes, `\` also quotes the character `"`.

The special meaning of keywords or aliases can be removed by quoting any character of the keyword. The recognition of function names or special command names listed below cannot be altered by quoting them.

## Arithmetic Evaluation

The ability to perform integer arithmetic is provided with the special command `let`. Evaluations are performed using long arithmetic. Constants take the form `[base#]n`, where base is a decimal number between two and thirty-six representing the arithmetic base and n is a number in that base. If base is omitted, base 10 is used.

An arithmetic expression uses the same syntax, precedence, and associativity of expression of the C language. All the integral operators, other than `++`, `--`, `?:`, and `,` are supported. Variables can be referenced by name within an arithmetic expression without using the parameter substitution syntax. When a variable is referenced, its value is evaluated as an arithmetic expression.

An internal integer representation of a variable can be specified with the `-i` option of the `typeset` special command. Arithmetic evaluation is performed on the value of each assignment to a variable with the `-i` attribute. If you do not specify an arithmetic base, the first assignment to the variable determines the arithmetic base. This base is used when parameter substitution occurs.

Since many of the arithmetic operators require quoting, an alternative form of the `let` command is provided. For any command beginning with `((`, all characters until the matching `))` are treated as a quoted expression. More precisely, `((...))` is equivalent to `let "..."`.

## Prompting

When used interactively, the shell prompts with the value of PS1 before reading a command. If at any time a new-line is typed and further input is needed to complete a command, the secondary prompt (the value of PS2) is issued.

## Conditional Expressions

A conditional expression is used with the `[[` compound command to test attributes of files and to compare strings. Word splitting and file name generation are not performed on the words between `[[` and `]]`. Each expression can be constructed from one or more of the following unary or binary expressions:

- `-a file`       True if file exists.
- `-b file`       True if file exists and is a block special file.
- `-c file`       True if file exists and is a character special file.
- `-d file`       True if file exists and is a directory.
- `-f file`       True if file exists and is an ordinary file.
- `-g file`       True if file exists and has its setgid bit set.
- `-h file`       True if file exists and is a symbolic link.
- `-k file`       True if file exists and has its sticky bit set.
- `-n string`     True if length of string is non-zero.
- `-o option`     True if option named option is on.
- `-p file`       True if file exists and is a fifo special file or a pipe.
- `-r file`       True if file exists and is readable by current process.
- `-s file`       True if file exists and has size greater than zero.
- `-t fildes`     True if file descriptor number fildes is open and associated with a terminal device.
- `-u file`       True if file exists and has its setuid bit set.
- `-w file`       True if file exists and is writable by current process.
- `-x file`       True if file exists and is executable by current process. If file exists and is a directory, the current process has permission to search in the directory.
- `-z string`     True if length of string is zero.
- `-H file`       True if file exists and is a hidden directory (see cdf(4)).

- `-L file`       True if file exists and is a symbolic link.
- `-O file`       True if file exists and is owned by the effective user ID of this process.
- `-G file`       True if file exists and its group matches the effective group ID of this process.
- `-S file`       True if file exists and is a socket.
- `file1 -nt file2`  True if file1 exists and is newer than file2.
- `file1 -ot file2`  True if file1 exists and is older than file2.
- `file1 -ef file2`  True if file1 and file2 exist and refer to the same file.

- `string = pattern`   True if string matches pattern.
- `string != pattern`  True if string does not match pattern.
- `string1 < string2`  True if string1 comes before string2 based on ASCII value of their characters.
- `string1 > string2`  True if string1 comes after string2 based on ASCII value of their characters.
- `exp1 -eq exp2`      True if exp1 is equal to exp2.
- `exp1 -ne exp2`      True if exp1 is not equal to exp2.
- `exp1 -lt exp2`      True if exp1 is less than exp2.
- `exp1 -gt exp2`      True if exp1 is greater than exp2.
- `exp1 -le exp2`      True if exp1 is less than or equal to exp2.
- `exp1 -ge exp2`      True if exp1 is greater than or equal to exp2.

A compound expression can be constructed from these primitives by using any of the following, listed in decreasing order of precedence.

- `(expression)`       True, if expression is true. Used to group expressions.
- `! expression`       True if expression is false.
- `expression1 && expression2`  True, if expression1 and expression2 are both true.
- `expression1 || expression2`  True, if either expression1 or expression2 is true.

## Input/Output

Before a command is executed, its input and output can be redirected using a special notation interpreted by the shell. The following can appear anywhere in a simple-command or can precede or follow a command and are not passed on to the invoked command. Command and parameter substitution occurs before word or digit is used, except as noted below. File name generation occurs only if the pattern matches a single file and blank interpretation is not performed.

- `<word`   Use file word as standard input (file descriptor 0).
- `>word`   Use file word as standard output (file descriptor 1). If the file does not exist, it is created. If the file exists, and the noclobber option is on, an error occurs; otherwise, the file is truncated to zero length.
- `>|word`  Same as `>`, except that it overrides the noclobber option.
- `>>word`  Use file word as standard output. If the file exists, output is appended to it (by first searching for the end-of-file); otherwise, the file is created.
