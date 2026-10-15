# EXAMPLE 13.13

```
1 $ export TERM=sun    # or declare -x TERM=sun
2 $ NAME="John Smith"
$ export NAME
$ echo $NAME
John Smith
3 $ echo $$
319                 # pid number for parent shell
4 $ bash             # Start a subshell
5 $ echo $$
340                 # pid number for new shell
6 $ echo $NAME
John Smith
7 $ declare -x NAME="April Jenner"
$ echo $NAME
April Jenner
8 $ exit              # Exit the subshell and go back to parent shell
9 $ echo $$
319                 # pid number for parent shell
10 $ echo $NAME
John Smith
```

# EXPLANATION

1 The TERM variable is assigned sun. The variable is exported at the same time. Now, processes started from this shell will inherit the variable. You can use declare -x to do the same thing.

2 The variable NAME is defined and exported to make it available to subshells started from the shell.

3 The value of this shell's PID is printed.

4 A new bash shell is started. The new shell is called the child. The original shell is its parent.

5 The PID of the new bash shell is stored in the $$ variable and its value is echoed.

6 The variable, set in the parent shell, was exported to this new shell and is displayed.

7 The built-in declare function is another way to set a variable. With the -x switch, declare marks the variable for export. The variable is reset to April Jenner. It is exported to all subshells, but will not affect the parent shell. Exported values are not propagated upward to the parent shell.

8 This bash child shell is exited.

9 The PID of the parent is displayed again.

10 The variable NAME contains its original value. Variables retain their values when exported from parent to child shell. The child cannot change the value of a variable for its parent.