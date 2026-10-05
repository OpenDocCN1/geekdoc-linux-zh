The -F option causes ls to print a slash (/) at the end of directory names and an asterisk (*) at the end of the names of executable files. In this example, the string that replaces the alias ll (-l) itself contains an alias (ls). When it replaces an alias with its value, the shell looks at the first of the replacement string to see whether it is an alias. In the preceding example, the replacement string contains the alias ls, a second substitution occurs to produce the final command ls -F -l. (To avoid a recursive plunge, the ls in the replacement text, although an alias, is not expanded a second time.)

When given a list of aliases without the =value or value, the alias responds by displaying the value of each defined alias. The alias builtin reports an error if an alias has not been defined:

```
$ alias 11 1 1 ls wx
alias 11='ls -l'
alias 1='ls -ltr'
alias ls='ls -F'
alias zap='rm -i'
bash: wx: command not found
```

You can avoid alias substitution by preceding the command with a backslash (\

```
$ \ls
Test_Emacs XTerm.ad flute.ps maptax.icn
Tiger fiext.icn floor testdir
```

Because the replacement of an alias name does not change the value of the command line, any arguments are received by the command that executes:

```
$ 11 fl
-rw-r-r-- 1 max group 641 2010-04-01 08:12 fiext.icn
-rw-r-r-- 1 max group 30015 2009-03-01 14:24 fiext.ps
-rwxr-xr-x 1 max group 485 2009-09-21 08:03 floor*
```

You can remove an alias with the alias builtin. When the zap alias is removed, it is no longer displayed with the alias builtin and its subsequent use results in an error message:

```
$ unalias zap
$ alias
alias 11='ls -l'
alias 1='ls -ltr'
alias ls='ls -F'
$ zap maptax.icn
bash: zap: command not found
```

# FUNCTIONS

A shell function is similar to a shell script in that it stores a series of commands for execution at a later time. However, because the shell stores a function in the computer’s main memory (RAM) instead of a file on the disk, it can access it more quickly than the shell can access a script. The shell also preprocesses (parses) a function so that it starts up quickly than a script. Finally the shell executes a