# 13.3.5 Multiple Commands at the Command Line

A command line can consist of multiple commands. Each command is separated by a semicolon, and the command line is terminated with a newline. The exit status is that of the last command in the chain of commands.

# EXAMPLE 13.22

```
$ ls; pwd; date
```

# EXPLANATION

The commands are executed from left to right, one after the other, until the newline is reached.

# 13.3.6 Command Grouping

Commands may also be grouped so that all of the output is either piped to another command or redirected to a file.

# EXAMPLE 13.23

```
$ ( ls; pwd; date ) > outfile
```

# EXPLANATION

The output of each of the commands is sent to the file called outfile. The spaces inside the parentheses are necessary.

# 13.3.7 Conditional Execution of Commands

With conditional execution, two command strings are separated by the special metacharacters, double ampersands (&&) and double vertical bars (||). The command on the right of either of these metacharacters will or will not be executed based on the exit condition of the command on the left.

# EXAMPLE 13.24

```
$ cc prgm1.c -o prgm1 && prgm1
```

# EXPLANATION

If the first command is successful (has a 0 exit status), the command after the && is executed; that is, if the cc program can successfully compile prgm1.c, the resulting executable program, prgm1, will be executed.