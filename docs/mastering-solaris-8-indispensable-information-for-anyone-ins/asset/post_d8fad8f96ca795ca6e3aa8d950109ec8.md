
Just as with the other shells, the Korn shell performs an evaluation of the variables on the command line. A closer look at the steps the Korn shell takes when using functions, aliases, input/output redirection, variable expansion, tilde expansion, and substitutions should make the ksh capabilities clearer. You can execute a script by using the script name as an argument. The following example demonstrates this:

```
$ ksh <scriptname>
```

This will call ksh even if you are in a Bourne or C Shell mode. If you want to execute the file containing the script, you can, with the correct permission, use the filename as a command, as in the following:

```
$ <filename>
```

If you use the symbols #! and follow that with the ksh path, the shell will run the script no matter what shell you call it from, as in the following example (unless you specify a different script):

```
#!/bin/ksh
```

## Korn Shell Variables

The Korn shell allows you to assign values to variables much like the Bourne shell does. Here is the syntax:

```
<VARIABLE>=value
```

> When assigning values to variables, do not leave space on either side of the equal sign. If you want to have spaces in your command, put quotes around the value or the space.

The conventions for referencing the value of a variable in the Korn shell are the same as they are in sh and csh. Precede the variable name with a dollar sign and enclose it in braces. The Korn shell refers to arguments on the command line by their position. It uses special variables such as $1, $2, and so on up to $9. Arguments past the ninth must have braces, as in ${10}.

In the Korn shell, the typeset built-in sets attributes. By using typeset, you can set for a variable attributes that control its value, such as readonly. To unset the value, you can use the unset built-in, which removes the variable’s value and attributes. The following example demonstrates how to assign a lowercase attribute:

```
$ typeset -l <TEXT>
$ <TEXT>="DEPARTMENT STORE"
$ ECHO $<TEXT>
department_store
```

The `typeset -l` assigns a lowercase attribute to the variable `<TEXT>`. You could do the opposite by assigning the `typeset -u` attribute to lowercase variables to produce output with uppercase letters.

Another useful feature of the Korn shell is that it gives you the ability to assign integer attributes when you want to do mathematical calculations on a variable. The shell will take a string variable, convert it internally to a number, work calculations on it, then convert it back into a string. The variable is stored as an integer, which makes calculations much quicker. Refer to the following example:

```
$ typeset -i COUNT
```

Because the integer built-in in ksh is so close in identity to `typeset -i`, you can use the following command:

```
$ integer COUNT
```

The Korn shell allows you to assign a base other than 10 to an integer variable. It will then display the variable. Here is the syntax:

```
typeset -I <base variable>
```

The `<base variable>` is the base you want to use in the calculation. If it’s more than 10, the value is displayed as `base#value`.

If a variable is given the `export` attribute, a copy of it is sent to all child processes. The Korn shell supports the `export` built-in and also provides `typeset -x` to set the `export` attribute. The `export` attribute may be set for functions as well as variables and will be available in subshells. All Korn shell variables that you create and use in a shell script are global once exported; therefore, they will be available in the current shell and in subshells as well. You may create variables that are local to a function, but they will be recognized only within that function.

> TIP When a function has a local variable with the same name as a global variable, all references within the function refer to the local variable. References outside the function refer to the global variable.

Caution should be used when naming variables. Because local variables may be used in a general way, and because scripts may be written by several different people, it is better to have unique names for variables within a function. To avoid naming confusion, you can use the `typeset` built-in to declare that a variable be local to the function it is defined in.

### Keyword Variables

Like the Bourne shell and the C shell, the Korn shell has inherited a set of keyword variables. Some have values that are set and can be changed by you. Others are absolute and cannot be changed. Some may have special meaning to the shell. Table 19.2 lists the keyword variables available to the Korn shell with brief descriptions of their functions or their use. Several will be new to you since they are available only in ksh. All are pre-defined by the `$` symbol when used in `script writing`.

**TABLE 19.2: KEYWORD VARIABLES IN THE KORN SHELL**

| Keyword | Description |
| :--- | :--- |
| `#` | Denotes number of command-line arguments |
| `*` | Makes all command-line arguments single arguments |
| `@` | Makes all command-line arguments individual arguments |
| `-` | Denotes last argument of previous command |
| `CDPATH` | Produces a list of absolute path names of directories searched by `cd` if set |
| `FCEEDIT` | Names the editor that the `fc` built-in uses |
| `FPATH` | Lists files that contain functions |
| `HISTFILE` | Stores history of filenames |
| `HISTFILESIZE` | Indicates the number of lines of history stored in HISTFILE |
| `HISTSIZE` | Indicates the number of events stored in the history list during a session |
| `HOME` | Gives the path name of your home directory |
| `IFS` | Denotes an Internal Field Separator |
| `LINENO` | Sets the value to the line number of the command it executes |
| `MAIL` | Denotes the file where your mail is stored |
| `OPTARG` | Denotes a variable set by the `getopts` built-in |
| `OPTIND` | Denotes a variable set by the `getopts` built-in |
| `PATH` | Denotes a list of directories searched for commands |
| `PPID` | Indicates the value of the PID (parent process) |
| `PS1` | Denotes a shell prompt string |
| `PS2` | Denotes a shell secondary prompt string |
| `LINES, COLUMNS, and PS3` | Control the format of output |
| `PS4` | Denotes a prompt string used in debugging; used with `set -x` |
| `OLDPWD` | Denotes an old, previous working directory |
| `PWD` | Denotes a previous working directory; may be toggled back with `OLDPWD` |
| `RANDOM` | Assigns a random integer value for testing, dummy data, etc. |
| `SECONDS` | Denotes an integer variable of number of seconds since start of shell session |
| `TMOUT` | Sets a time to exit shell after elapsed seconds |

The Korn shell uses the underscore (_) to refer to specific arguments and not the symbols on the command line. This example demonstrates how the underscore is used:

```
$ cat box1 box2 box3 > al13boxes
$ echo $_
box3
```

The Korn shell refers to the last argument of the previous simple command, which is box3 in the output.

## Built-In Variables

The Korn shell allows you to use a larger set of built-ins than do the Bourne and C shells. These built-in variables include sets for option processing, input/output, control flow, and control of the user's environment. Korn shell built-in commands are shown in Table 19.3. Most of the keyword variables will be discussed further later in this chapter. Examples will be given so that you may try out the scripts while you become more familiar with keyword variables.

TABLE 19.3: KORN SHELL BUILT-IN COMMANDS

| Command | Description |
| :--- | :--- |
| ( ) | Subshell, creates a copy of itself |
| $( ) | Command substitution, a command executed from within a subshell |
| (( )) | Assignment operator (used with an enclosed equal sign) |
| $(( )) | Expression evaluation, not used with an equal sign |
| [ ] | Test command |
| [[ ]] | String comparisons, adds strings that match |

As discussed in Chapter 18, parentheses are used to group commands. The Korn shell will create a copy of itself (a subshell) for each group of commands and a new process to execute each command. Each subshell will have its own set of variables with values that may or may not be different from the values of the variables in other subshells. The following example demonstrates how a subshell is created and executed:

```
#! (s1x ; ten) & d &
```

Tasks six and ten will be executed sequentially in the background, and task d will be run in the background at the same time.
