+   b.
+       $ pwd
+       /home/zach/grants
+       $ CDPATH=\$(pwd)
+       $ cd \$HOME/biblios

7. Name two ways you can identify the PID number of the login shell.

8. Give the following command:

    $ sleep 30 | cat /etc/inittab

    Is there any output from sleep? Where does cat get its input from? What has to happen before the shell displays another prompt?

# ## ADVANCED EXERCISES

9. Write a sequence of commands or a script that demonstrates variable expansion occurs before pathname expansion.

10. Write a shell script that outputs the name of the shell executing it.

11. Explain the behavior of the following shell script:

```
$ cat quote_demo
twoliner="This is line 1.
This is line 2."
echo "$twoliner"
echo $twoliner
```

+   a. How many arguments does each echo command see in this script? Explain.
+   
+   b. Redefine the IFS shell variable so that the output of the second echo is the same as the first.

12. Add the exit status of the previous command to your prompt so that it behaves similarly to the following:

    $ [0] ls xxx
    15: xxx: No such file or directory
    $ [1]

13. The dirname utility treats its argument as a pathname and writes to standard output the path prefix—that is, everything up to but not including the last component:

    $ dirname a/b/c/d
    a/b/c

    If you give dirname a simple filename (no / characters) as an argument, dirname writes a . to standard output: