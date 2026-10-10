and turning the command list into a process list created a subshell to execute the commands.

# NOTE

> A process list is a command grouping type. Another command grouping type puts the commands between curly brackets and ends the command list with a semicolon (;). The syntax is as follows: `{ command; }`. Using curly brackets for command grouping does not create a subshell as a process list does.

To indicate if a subshell was spawned, a command using an environment variable is needed here. (Environment variables are covered in detail in [Chapter 6](#). The command needed is `echo $BASH_SUBSHELL`. If it returns `0`, then there is no subshell. If it returns `1` or more, a subshell was created.

First, the example using just a command list is executed with the `echo $BASH_SUBSHELL` tacked onto the end:

```
```bash
$ pwd ; ls test* ; cd /etc ; pwd ; cd ; pwd ; ls my* ; echo $BASH_SUBSHELL
/home/christine
test_file  test_one  test_two
/etc
/home/christine
my_file  my_scrap  my_scripy
0
$ 
```
```

At the very end of the commands' output, you can see the number zero (0) is displayed. This indicates a subshell was not created to execute these commands.

The results are different using a process list. The list is executed with `echo $BASH_SUBSHELL` tacked onto the end:

```
```bash
$ (pwd ; ls test* ; cd /etc ; pwd ; cd ; pwd ; ls my* ; echo $BASH_SUBSHELL)
/home/christine
```
```