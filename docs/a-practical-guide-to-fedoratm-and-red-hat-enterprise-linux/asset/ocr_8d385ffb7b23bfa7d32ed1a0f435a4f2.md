+   a. What do you have to do to the script to be able to execute it?
+   b. Why does the script use the **read** builtin the first time it accepts input from the terminal and the **cat** utility the second time?

6. Assume the `/home/zach/grants/biblio s` and `/home/zach/biblios` directories exist. Specify Zach’s working directory after he executes each sequence of commands. Explain what happens in each case.

+   a.
+   ```
+   $ pwd
+   /home/zach/grants
+   $ CDPATH=$ (pwd)
+   $ cd
+   $ cd bibli os
+   ```
+   b.
+   ```
+   $ pwd
+   /home/zach/grants
+   $ CDPATH=$ (pwd)
+   $ cd $HOME/bibli os
+   ```

7. Name two ways you can identify the PID number of the login shell.

8. Enter the following command:
```
$ sleep 30 | cat /etc/services
```
Is there any output from **sleep**? Where does **cat** get its input from? What has to happen before the shell will display a prompt?

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

+   a. How many arguments does each **echo** command see in this script? Explain.
+   b. Redefine the **IFS** shell variable so the output of the second **echo** is the same as the first.

12. Add the exit status of the previous command to your prompt so it behaves similarly to the following:
```
$ [0] ls xxx
ls: xxx: No such file or directory
$ [1]
```