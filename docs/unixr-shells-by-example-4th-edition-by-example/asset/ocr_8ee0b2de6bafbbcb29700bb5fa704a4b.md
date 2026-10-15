# EXAMPLE 8.28

(The Command Line)

```
$ greet Dee Bert Lizzy Tommy
Hi Dee
Hi Bert
Hi Lizzy
Hi Tommy
```

# EXPLANATION

+   1. $* and $@ expand to a list of all the positional parameters, in this case, the arguments passed in from the command line: Dee, Bert, Lizzy, and Tommy. Each name in the list will be assigned, in turn, to the variable name in the for loop.
+   2. The commands in the body of the loop are executed until the list is empty.
+   3. The done keyword marks the end of the loop body.

# EXAMPLE 8.29

(The Script)

```
#!/bin/sh
# Scriptname: permx
1 for file # Empty wordlist
do
2 if [ -f $file -a ! -x $file ]
then
3   chmod +x $file
    echo $file now has execute permission
fi
done
```

(The Command Line)

```
4 $ permx *
addon now has execute permission
checkon now has execute permission
do it now has execute permission
```

# EXPLANATION

+   1. If the for loop is not provided with a wordlist, it iterates through the positional parameters. This is the same as for file in $*.
+   2. The filenames are coming in from the command line. The shell expands the asterisk (*) to all filenames in the current working directory. If the file is a plain file and does not have execute permission, line 3 is executed.
+   3. Execute permission is added for each file being processed.
+   4. At the command line, the asterisk will be evaluated by the shell as a wildcard and all files in the current directory will be replaced for the *. The files will be passed as arguments to the permx script.