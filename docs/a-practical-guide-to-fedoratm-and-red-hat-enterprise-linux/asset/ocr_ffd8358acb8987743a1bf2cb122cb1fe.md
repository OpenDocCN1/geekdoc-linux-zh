The next command line executes a list that runs three commands as background jobs. The shell displays a shell prompt immediately:

```
$ d & e & f &
[1] 14290
[2] 14291
[3] 14292
```

The next example uses a pipeline symbol to send the output from one command to the next command and an ampersand (&) to run the entire pipeline in the background. Again the shell displays the prompt immediately. The shell commands that are part of a pipeline form a single job. That is, the shell treats a pipeline as a single job, no matter how many commands are connected using pipeline (\|) symbols or how complex they are. The Bourne Again Shell reports only one process in the background (although there are three):

```
$ d \| e \| f &
[1] 14295
```

# ## && AND || BOOLEAN CONTROL OPERATORS

The && (AND) and || (OR) Boolean operators are called short-circuiting control operators. If the result of using one of these operators can be decided by looking only at the left operand, the right operand is not evaluated. The result of a Boolean operator is either 0 (true) or 1 (false).

+   - The && operator causes the shell to test the exit status of the command preceding it. If the command succeeds, bash executes the next command; otherwise, it skips the next command. You can use this construct to execute commands conditionally.

```
$ mkdir bkup && cp -r src bkup
```

This compound command creates the directory bkup. If mkdir succeeds, the content of directory src is copied recursively to bkup.

+   - The || control operator also causes bash to test the exit status of the first command but has the opposite effect: The remaining command(s) are executed only if the first command failed (that is, it exited with nonzero status).

```
$ mkdir bkup \|\| echo "mkdir of bkup failed" >> /tmp/log
```

The exit status of a command list is the exit status of the last command in the list. You can group lists with parentheses. For example, you could combine the previous two examples as

```
$ (mkdir bkup && cp -r src bkup) \|\| echo "mkdir failed" >> /tmp/log
```

In the absence of parentheses, && and || have equal precedence and are grouped from left to right. The following examples use the true and false utilities. These utilities do nothing and return true (0) and false (1) exit statuses, respectively:

```
$ false; echo $?
1
```