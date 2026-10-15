# EXPLANATION (CONTINUED)

+   4 The functions alias lists all functions and their definitions.
+   5 The hash alias lists all tracked aliases.
+   6 The history alias lists and numbers all commands in the history file, .sh_history.
+   7 The integer alias allows you to create integer-type variables.
+   8 The r alias lets you redo a previous command from the history list.
+   9 The stop alias causes a process to be suspended if a job number or PID is provided to the kill command. The job can be resumed in the foreground by typing fg.
+   10 The suspend alias suspends the current job by sending the STOP signal and the PID ($$) of this process to the kill command.
+   11 The true alias is set to the do-nothing command, often used to start an infinite loop.
+   12 The type alias indicates the type of command you are executing: an alias, a binary executable, and so forth.

# 11.5.2 Creating Aliases

The user can create aliases in the Korn shell. An alias is a nickname for an existing command or commands. The real command(s) is substituted for the alias when the shell evaluates the command line.

# EXAMPLE 11.22

```
1 $ alias c1='clear'
2 $ alias l='ls -laF'
3 $ alias ls='ls -aF'
4 $ \ls ..
```

# EXPLANATION

+   1 The alias c1 is an alias for clear.
+   2 The alias l is 1. The letter l is a nickname for the command ls -laF.
+   3 The alias ls is assigned the command ls -aF.
+   4 The backslash turns off the meaning of the alias for the execution of this line. The real ls command, not the alias, is executed.

# 11.5.3 Deleting Aliases

The unalias command deletes an alias.

# EXAMPLE 11.23

```
unalias c1
```

# EXPLANATION

The alias c1 is removed from the list of set aliases.