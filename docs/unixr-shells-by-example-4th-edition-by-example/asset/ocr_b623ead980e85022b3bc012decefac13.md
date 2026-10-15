# EXPLANATION

+   1. The contents of filex are displayed on the screen.
+   2. The output of the date command is redirected to filex. The file is truncated and its original contents overwritten.
+   3. The contents of filex are displayed.
+   4. The noclobber variable is set.
+   5. Since filex already exists and noclobber is set, the shell reports that the file exists and will not allow it to be overwritten.
+   6. The output of ls is redirected to filex because the >! operator overrides the effects of noclobber.
+   7. The effects of the >! symbol were temporary. It does not turn off noclobber. It simply overrides noclobber for the command where it is implemented.
+   8. The noclobber variable is unset.

# 9.10 Variables

C/TC shell variables hold only strings or a set of strings. Some variables are built into the shell and can be set by turning them on or off, such as the noclobber or filec variable. Others are assigned a string value, such as the path variable. You can create your own variables and assign them to strings or the output of commands. Variable names are case sensitive and may contain up to 20 characters consisting of numbers, letters, and the underscore.

There are two types of variables: local and environment. Local variables are created with the set command. Global variables are created with the setenv command. The scope of a variable is its visibility. A local variable is visible to the shell where it is defined. The scope of environment variables is often called global. Their scope is for this shell and all processes spawned (started) from this shell.

The dollar sign ($) is a special metacharacter that, when preceding a variable name, tells the shell to extract the value of that variable. The echo command, when given the variable as an argument, will display the value of the variable after the shell has processed the command line and performed variable substitution.

The special notation $? when prepended to the variable name, lets you know whether the variable has been set. If a one is returned, it means true, the variable has been set. If a zero is returned, it means false, the variable has not been set.

# EXAMPLE 9.46

```
1 % set filec
2 % set history = 50
3 % set name = George
4 % set machine = `uname -n`
5 % echo $?machine
1
6 % echo $?blah
0
```