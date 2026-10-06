# Compatibility Summary 319

of the current and previous directories, respectively. ~+ and -- are not supported by the POSIX standard shell.

```
$ pwd
/usr/spool/uucpublic/steve
$ cd
$ pwd
/users/pat
$ echo +
/users/pat
$ echo --
/usr/spool/uucpublic/steve
$
```

In addition to the preceding substitutions, the shell also checks for a tilde after a colon : and performs tilde substitution on that as well (that's how you can have something like ~/bin in your PATH and have it work correctly).

# Order of Search

It's worthwhile understanding the search order the shell uses when you type in a command name:

+   1. The shell first checks to see whether the command is a reserved word (such as for or do).
2. If it's not a reserved word and not quoted, the shell next checks its alias list, and if it finds a match, performs the substitution. If the alias definition ends in a space, it also attempts alias substitution on the next word. The final result is then checked against the reserved word list, and if it's not a reserved word, the shell proceeds to step 3.
3. The shell checks the command against its function list and executes the eponymous function found.
4. The shell checks to see whether the command is a built-in command (such as cd and pwd).
5. Finally, the shell searches the PATH to locate the command.
6. If the command still isn't found, a “command not found” error message is issued.

# Compatibility Summary

Table 14.4 summarizes the compatibility of the POSIX standard shell, the Korn shell, Bash with the features described in this chapter. In this table, an “X” denotes a supported feature, “UP,” an optional feature in the POSIX shell (these are also known as “User Portability” features in the POSIX shell specification), and “POS” a feature supported only by Bash when it is invoked with the name sh or with the --posix command-line option, or after set -o posix is executed.