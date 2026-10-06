# Advanced Bash–Scripting Guide

exit

Unconditionally terminates a script. The exit command may optionally take an integer argument, which is returned to the shell as an exit status of the script. It is a good practice to end all the simplest scripts with an exit 0, indicating a successful run.

If a script terminates with an exit lacking an argument, the exit status of the last command executed in the script, not counting the exit.

exec

This builtin replaces the current process with a specified command. Normally, when the shell encounters an exec echo [26] a child process to actually execute the command. Using the exec builtin, it does not fork, and the command'ed replaces the shell. When used in a script, it forces an exit from the script when the exec command terminates. For a reason, if an exit appears in a script, it would be the final command.

An exec also serves to reassign file descriptors exec <zzz-file replaces stdin with the file zzz-file (see Example 16–1).

# Example 11–15. Effects of exec

![](bbox=[0.0, 0.0, 0.0, 0.0])

```
```
#!/bin/bash
exec echo "Exiting \"0\"" # Exit from script.

# The following lines never execute.
echo "This will never echo."

exit 0 # Will not exit here.
```
```

The --exec option to find is not the same as the exec shell builtin.

shopt

This command permits changing shell options on the fly (see Example 24–1 and Example 24–2). It often appears in the Bash startup files, but also has its uses in scripts. Needs version 2 or later of Bash.

```
```
shopt -s cdspell
# Allows minor misspelling directory names with 'cd'
command.
```
```

# Commands

true

Chapter 11. Internal Commands and Built

135