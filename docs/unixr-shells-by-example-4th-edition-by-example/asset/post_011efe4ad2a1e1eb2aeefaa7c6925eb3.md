
## EXPLANATION
- 1 The variable name is assigned the string Jody.
- 2 The double quotes surrounding the string will protect all special metacharacters from interpretation, with the exception of $ in $name. Variable substitution is performed within double quotes.
- 3 Variable substitution and command substitution are both performed when enclosed within double quotes. The variable name is expanded, and the command in backquotes, date, is executed.

## 7.8 Command Substitution

When a command is enclosed in backquotes, it will be executed and its output returned. This process is called command substitution. It is used when assigning the output of a command to a variable or when substituting the output of a command within a string. All three shells use backquotes to perform command substitution.

## EXAMPLE 7.34

```
1 $ name=`nawk -F: '{print $1}' database`
$ echo $name
Ebenezer Scrooge
2 $ set `date`
3 $ echo $*
Fri Oct 22 09:35:21 PDT 2004
4 $ echo $2 $6
Oct 2004
```

## EXPLANATION
- 1 The nawk command is enclosed in backquotes. Command substitution is performed. The output is assigned to the variable name, as a string, and displayed.
- 2 The set command assigns the output of the date command to positional parameters. Whitespace separates the list of words into its respective parameters.
- 3 The $* variable holds all of the positional parameters. The output of the date command was stored in the $* variable. Each parameter is separated by whitespace.
- 4 The second and sixth parameters are printed.

## EXAMPLE 7.36 (CONTINUED)

```
3 $ welcome () { echo "Hi $1 and $2"; }
4 $ welcome tom joe
Hi tom and joe
5 $ set jane nina lizzy
6 $ echo $*
jane nina lizzy
7 $ welcome tom joe
hi tom and joe
8 $ echo $1 $2
jane nina
```

## EXPLANATION
1 The function fun is named and defined. The name is followed by a list of commands enclosed in curly braces. Each command is separated by a semicolon. A space is required after the first curly brace or you will get a syntax error. A function must be defined before it can be used.

2 The function behaves just like a script when invoked. Each of the commands in the function definition are executed in turn.

3 There are two positional parameters used in the function welcome. When arguments are given to the function, the positional parameters are assigned those values.

4 The arguments to the function, tom and joe, are assigned to $1 and $2, respectively. The positional parameters in a function are private to the function and will not interfere with any used outside the function.

5 The positional parameters are set at the command line. These variables have nothing to do with the ones set in the function.

6 $* displays the values of the currently set positional parameters.

7 The function welcome is called. The values assigned to the positional parameters are tom and joe.

8 The positional variables assigned at the command line are unaffected by those set in the function.

## 7.9.2 Listing and Unsetting Functions

To list functions and their definitions, use the set command. The function and its definition will appear in the output, along with the exported and local variables. Functions and their definitions are unset with the unset command.

## 7.10 Standard I/O and Redirection

When the shell starts up, it inherits three files: stdin, stdout, and stderr. Standard input normally comes from the keyboard. Standard output and standard error normally go to the screen. There are times when you want to read input from a file or send output or error to a file. This can be accomplished by using I/O redirection. See Table 7.9 for a list of redirection operators.

## Table 7.9 Redirection Operators

| Operator | What It Does |
|---|---|
| < | Redirect input |
| > | Redirect output |
| >> | Append output |
| 2> | Redirect error |
| 1>&2 | Redirect output to where error is going |
| 2>&1 | Redirect error to where output is going |

## EXAMPLE 7.37

```
1 $ tr '[A-Z]' '[a-z]' < myfile    # Redirect input
2 $ ls > lsfile                  # Redirect output
$ cat lsfile
dir1
dir2
file1
file2
file3
3 $ date >> lsfile               # Redirect and append output
$ cat lsfile
dir1
dir2
file1
file2
file3
Mon Sept 20 12:57:22 PDT 2004
4 $ cc prog.c 2> errfile         # Redirect error
5 $ find . -name \*.c -print > foundit 2> /dev/null   # Redirect output to foundit,
# and error to /dev/null
6 $ find . -name \*.c -print > foundit 2>&1   # Redirect output and send standard
# error to where output is going
7 $ echo "File needs an argument" 1>&2   # Send standard output to error
```
