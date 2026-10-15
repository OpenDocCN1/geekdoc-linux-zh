
**Table 11.14 Other Uses of the typeset Command**

| Command | What It Does |
|---|---|
| `typeset` | Displays all variables |
| `typeset -i num` | Will only accept integer values for num |
| `typeset -x` | Displays exported variables |
| `typeset a b c` | If defined in a function, creates a, b, and c to be local variables |
| `typeset -r x=foo` | Sets x to foo and then makes it read-only |

## 11.9.10 Positional Parameters

Normally the special built-in variables, often called positional parameters, are used in shell scripts when passing arguments from the command line, or used in functions to hold the value of arguments passed to the function. The variables are called positional parameters because they are referenced by numbers 1, 2, 3, and so on, representing their respective positions in the parameter list. See Table 11.15.

The name of the shell script is stored in the $0 variable. The positional parameters can be set and reset with the set command.

**Table 11.15 Positional Parameters**

| Expression | Function |
|---|---|
| `$0` | References the name of the current shell script |
| `$1-$9` | Positional parameters 1-9 |
| `${10}` | Positional parameter 10 |
| `$#` | Evaluates to the number of positional parameters |
| `$*` | Evaluates to all the positional parameters |
| `$@` | Same as `$*`, except when double quoted |
| `"$*"` | Evaluates to "$1 $2 $3", and so on |
| `"$@"` | Evaluates to "$1" "$2" "$3", and so on |

### EXAMPLE 11.32

```sh
1  $ set tim bill ann fred
    $ print $*        # prints all the positional parameters.
    tim bill ann fred

2  $ print $1        # Prints the first position.
    tim

3  $ print $2 $3     # Prints the second and third position.
    bill ann

4  $ print $#        # Prints the total number of positional parameters.
    4

5  $ set a b c d e f g h i j k l m
    $ print $10      # Prints the first positional parameter followed by a 0.
    a0
    $ print ${10} ${11} # Prints the 10th and 11th positions.
    j k

6  $ print $#
    13

7  $ print $*
    a b c d e f g h i j k l m

8  $ set file1 file2 file3
    $ print \$$#
    $3

9  $ eval print \$$#
    file3
```

### EXPLANATION

- **1.** The set command assigns values to positional parameters. The $* special variable contains all of the parameters set.
- **2.** The value of the first positional parameter, tim, is displayed.
- **3.** The value of the second and third parameters, bill and ann, are displayed.
- **4.** The $# special variable contains the number of positional parameters currently set.
- **5.** The set command resets all of the positional parameters. The original parameter list is cleared. To print any positional parameters beyond 9, the curly braces are used to keep the two digits together. Otherwise, the value of the first positional parameter is printed, followed by the number appended to it.
- **6.** The number of positional parameters is now 13.
- **7.** The values of all of the positional parameters are printed.
- **8.** The dollar sign is escaped; $# is the number of arguments. The print command displays $3, a literal dollar sign followed by the number of positional parameters.
- **9.** The eval command parses the command line a second time before executing the command. The first time parsed by the shell, the print would display $3; the second time, after eval, the print displays the value of $3, file3.

## 11.9.11 Other Special Variables

The Korn shell has some special built-in variables, as shown in Table 11.16.

**Table 11.16 Special Variables**

| Variable | Meaning |
|---|---|
| `$$` | PID of the shell |
| `$-` | ksh options currently set |
| `$?` | Exit value of last executed command |
| `$!` | PID of last job put in background |

### EXAMPLE 11.33

```sh
1 $ print The pid of this shell is $$
The pid of this shell is 4725
2 $ print The options for this korn shell are $-
The options for this korn shell are ism
3 $ grep dodo /etc/passwd
$ print $?
1
4 $ sleep 25 &
[1] 400
$ print $!
400
```

### EXPLANATION

- **1.** The $$ variable holds the value of the PID for this process.
- **2.** The $- variable lists all options for this interactive Korn shell.
- **3.** The grep command searches for the string dodo in the /etc/passwd file. The `$?` variable holds the exit status of the last command executed. Because the value returned from grep is 1, grep is assumed to have failed in its search. An exit status of 0 indicates a successful exit.
- **4.** The & appended to the sleep command causes the command to be executed in the background. The $! variable holds the PID of the last command placed in the background.
