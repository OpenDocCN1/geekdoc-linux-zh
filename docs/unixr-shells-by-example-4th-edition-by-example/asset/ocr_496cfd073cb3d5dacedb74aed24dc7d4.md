# EXAMPLE 14.36 (CONTINUED)

```
(The Command Line)
4 $ perms *
addon now has execute permission
checkout now has execute permission
do it now has execute permission
```

# EXPLANATION

+   1 If the for loop is not provided with a wordlist, it iterates through the positional parameters. This is the same as for file in $*.
+   2 The filenames are coming in from the command line. The shell expands the asterisk (*) to all filenames in the current working directory. If the file is a plain file and does not have execute permission, line 3 is executed.
+   3 Execute permission is added for each file being processed.
+   4 At the command line, the asterisk will be evaluated by the shell as a wildcard and all files in the current directory will be replaced for the *. The files will be passed as arguments to the permx script.

# 14.6.3 The while Command

The while command evaluates the command following it and, if its exit status is 0, the commands in the body of the loop (commands between do and done) are executed. When the done keyword is reached, control is returned to the top of the loop and the while command checks the exit status of the command again. Until the exit status of the command being evaluated by the while becomes nonzero, the loop continues. When the exit status reaches nonzero, program execution starts after the done keyword.

# FORMAT

```
while command
do
    command(s)
done
```

# EXAMPLE 14.37

```
(The Script)
#!/bin/bash
# Scriptname: num
1 num=0    # Initialize num
```