# EXPLANATION (CONTINUED)

+   4 If the grep program cannot find the pattern, it returns an exit status of 1.
+   5 The grep program fails because the /etc/passwd file cannot be opened.
+   6 If grep cannot find the file, it returns an exit status of 2.

# 7.3.2 Multiple Commands at the Command Line

A command line can consist of multiple commands. Each command is separated by a semicolon, and the command line is terminated with a newline.

# EXAMPLE 7.9

```
$ ls; pwd; date
```

# EXPLANATION

The commands are executed from left to right, one after the other, until the newline is reached.

# Grouping Commands.

Commands may also be grouped so that all of the output is either piped to another command or redirected to a file.

# EXAMPLE 7.10

```
$ ( ls ; pwd; date ) > outfile
```

# EXPLANATION

The output of each of the commands is sent to the file called outfile. The spaces inside the parentheses are necessary.

# 7.3.3 Conditional Execution of Commands

With conditional execution, two command strings are separated by the special metacharacters, double ampersands (&&) and double vertical bars (||). The command on the right of either of these metacharacters will or will not be executed based on the exit condition of the command on the left.

# EXAMPLE 7.11

```
$ cc prgn1.c -o prgn1 && prgn1
```

# EXPLANATION

If the first command is successful (has a 0 exit status), the command after the && is executed; that is, if the cc program can successfully compile prgn1.c, the resulting executable program, prgn1, will be executed.