
## Table 13.14 bash Environment Variables (continued)

| Variable Name | Meaning |
|---|---|
| SHELL | When the shell is invoked, it scans the environment for this name. The shell gives default values to PATH, PS1, PS2, MAILCHECK, and IFS. HOME and MAIL are set by login(1). |
| SHELLOPTS | Contains a list of enabled shell options, such as braceexpand, hashall, monitor, etc. |
| SHLVL | Incremented by one each time an instance of bash is started. |
| TMOUT | Specifies number of seconds to wait for input before exiting. |
| UID | Expands to the user ID of the current user, initialized at shell startup. |

a. Not available in bash versions prior to 2.x.

## Setting Environment Variables.

To set environment variables, the export command is used either after assigning a value or when the variable is set. (See Table 13.15.) The declare built-in, given the -x option, will do the same. (Do not use the $ on a variable when exporting it.)

## FORMAT

```
export variable=value
variable=value; export variable
declare -x variable=value
```

## EXAMPLE 13.34

```
export NAME=john
PS1='\d\W\$USER\$ ' ; export PS1
declare -x TERM=sun
```

## Table 13.15 The export Command and Its Options

| Option | Value |
|---|---|
| -- | Marks the end of option processing; the remaining parameters are arguments. |
| -f | Name-value pairs are treated as functions, not variables. |
| -n | Converts a global (exported) variable to a local variable. The variable will not be exported to child processes. |
| -p | Displays all the global variables. |

## EXAMPLE 13.13

```
1 $ export TERM=sun    # or declare -x TERM=sun
2 $ NAME="John Smith"
$ export NAME
$ echo $NAME
John Smith
3 $ echo $$
319                 # pid number for parent shell
4 $ bash             # Start a subshell
5 $ echo $$
340                 # pid number for new shell
6 $ echo $NAME
John Smith
7 $ declare -x NAME="April Jenner"
$ echo $NAME
April Jenner
8 $ exit              # Exit the subshell and go back to parent shell
9 $ echo $$
319                 # pid number for parent shell
10 $ echo $NAME
John Smith
```

## EXPLANATION

1 The TERM variable is assigned sun. The variable is exported at the same time. Now, processes started from this shell will inherit the variable. You can use declare -x to do the same thing.

2 The variable NAME is defined and exported to make it available to subshells started from the shell.

3 The value of this shell's PID is printed.

4 A new bash shell is started. The new shell is called the child. The original shell is its parent.

5 The PID of the new bash shell is stored in the $$ variable and its value is echoed.

6 The variable, set in the parent shell, was exported to this new shell and is displayed.

7 The built-in declare function is another way to set a variable. With the -x switch, declare marks the variable for export. The variable is reset to April Jenner. It is exported to all subshells, but will not affect the parent shell. Exported values are not propagated upward to the parent shell.

8 This bash child shell is exited.

9 The PID of the parent is displayed again.

10 The variable NAME contains its original value. Variables retain their values when exported from parent to child shell. The child cannot change the value of a variable for its parent.

## 13.10.6 Unsetting Variables

Both local and environment variables can be unset by using the unset command, unless the variables are set as read-only.

## EXAMPLE 13.56

```
unset name; unset TERM
```

## EXPLANATION

The unset command removes the variable from the shell's memory.

## 13.10.7 Printing the Values of Variables

The echo Command. The built-in echo command prints its arguments to standard output. Echo, with the -e option, allows the use of numerous escape sequences that control the appearance of the output. Table 13.16 lists the echo options and escape sequences.

## Table 13.16 echo Options and Escape Sequences

| Option | Meaning |
|---|---|
| -e | Allows interpretation of the escape sequences shown below |
| -E | Disables the interpretation of these escape characters, even on systems where they are interpreted by defaultᵃ |
| -n | Suppresses newline at the end of a line of output |

**Escape Sequence**
| \a | Alert (bell)ᵃ |
| \b | Backspace |
| \c | Prints the line without a newline |
| \f | Form feed |
| \n | Newline |
| \r | Return |
| \t | Tab |
| \v | Vertical tab |
| \\ | Backslash |
| \nnn | The character whose ASCII code is nnn (octal) |

a. Not available in bash versions prior to 2.x.
