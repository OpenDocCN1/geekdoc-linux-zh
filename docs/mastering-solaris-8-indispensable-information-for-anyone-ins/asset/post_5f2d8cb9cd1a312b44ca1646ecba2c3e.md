
## Figure 18.1: Flow of the `if` command

Figure 18.1 illustrates the flow of the `if` command. The `fi` command is simply *if* spelled backwards; it marks the end of the `if` structure.

![](img/256e02a6afce528d264a8d911fa0ff20_716_0.png)

The shell will take this statement and, if the first argument is true, pass it on to the `then` statement and execute the command. If the statement is false, the control structure will end.

> **WARNING** The `test` built-in returns the results in the `if..then` statement. You should not use the word `test` as a script name. Solaris will treat it as a utility and your results will not be dependable.

In the following script, follow the flow of the `if` statement and check your results. You will be prompted for two words, which will be read in. The shell will use the `if` structure to evaluate the result returned by `testcase`. If `testcase` is true, then the command will be executed. Placing double quotes around each of the arguments ensures that the `test` utility works correctly in the event that you enter a space or special character:

```bash
$ cat ify
echo "testcase 1: \c"
read testcase1
echo "testcase 2: \c"
read testcase2
if [ "$testcase1" = "$testcase2" ]
then
    echo "Same"
fi
echo 'The End!'
```

```bash
$ ify
testcase 1:  testcase 1
testcase 2:  testcase 1
Same
The end!
```

In this example, the test built-in returns a true status if the first and third arguments are matched strings. The shell would then execute the commands between the `then` and `fi`. If a false status is returned, the shell passes control to the statement after `fi` and does not execute the statements between `then` and `fi`. In this case, that means that if both words are the same, the script will display `Same`.

The following example shows the same program with different input. It goes directly to `The end!`, skipping `Same` because the two did not match:

```bash
$ ify
testcase 1:  testcase 1
testcase 2:  testcase 2
The end!
$
```

The `test` built-in is also a utility in the Bourne shell. It may stand alone and be kept in `/usr/bin/test`. In place of the word `test`, you can use square brackets `[ ]`, which results in less confusion when writing scripts. You can use the built-in version if available or the utility if it is not. You can use the `type` built-in to determine whether you are using a built-in or standalone utility:

```bash
$ type test cat echo read
test is a shell builtin
cat is hashed (/bin/cat)
echo is a shell builtin
read is a shell builtin
```

You can get more information by using the `man` command before the name of the utility. Type `man` followed by the name of the shell and the shell will look up the built-ins. Table 18.1 lists the built-ins that are available in the Bourne shell. Chapter 19 includes a list of built-ins for the Korn shell and Chapter 20 includes a list of built-ins for the C shell.

## TABLE 18.1: BOURNE SHELL BUILT-INS

| Built-In | Description |
| :--- | :--- |
| `alias (unalias)` | Creates or removes a pseudonym or shorthand for a command or series of commands. |
| `bg` | Background; controls process execution. |
| `break` | Used to exit from a `for` or enclosing `while` loop, if one is executing. If you specify `n` (a number), then that many levels of looping is terminated. |
| `case` | Allows user a choice from a list of actions by evaluating a series of true and false statements. The first true response is executed, ending the case statement. |
| `cd` | Changes the working directory. |
| `chdir` | Same as `cd`. |
| `continue` | Allows escape from or advance within an enclosing `while`, `for`, `foreach`, or `until` loop. |
| `echo` | Causes arguments to be separated by blanks and terminated by a newline to standard output. |
| `eval` | Allows arguments to the `eval` command to be read as input to the shell and executes the resulting commands. |
| `exec` | Specified by arguments; executes in place of the shell without creating a new process. Input/output arguments may appear and, if no other arguments are given, cause the shell input/output to be modified. |
| `exit` | Causes the calling shell or shell script to exit. |
| `export` | Sends the variable and its value to the shell environment, causing its value to be set and used by all other commands until the `unset` command is used. |
| `[..]` | When used in a loop or as a control, it is a shortcut for the `test` built-in. |
| `[...]` | When used in file access, it can be used to match one of a set (abc) or a range (a-c) of characters. (i.e., `'ls [cbj]at'`, which would find `cat` and `bat` but not `nat`). |
| `fg` | Foreground; controls process execution. Also brings a job to the foreground. |
| `for` | Repeatedly executes an action a specified number of times. |
| `getopts` | Retrieves options and option arguments from a list of parameters. |
| `hash` | Recalculates the internal hash table of the contents of the directories listed in the path environmental variable to account for new commands added. |
| `if` | Control structure; a test statement that evaluates to true or false and then either executes an action or exits if the test condition is false. Also used with `then`, `else`, or `elif` to evaluate statements true or false. |
| `jobs` | Reports all jobs that are stopped or executing in the background. |
| `kill` | Terminates a process that you specify as an argument using the PID number or job ID. |
| `login` | Establishes the user and their associated group and environment based on a name and password given; the same as the command `su - <username>`. |
| `logout` | Used to exit from a login session. |
| `newgrp` | Used to log in to a new group. Changes your real and effective group ID; user stays logged in but a new shell is spawned. |
| `pwd` | Returns the present working directory. |
| `read` | Reads a line from standard input. |
| `readonly` | Shell built-in that protects the value of a given variable from reassignment. |
| `return` | Enables the execution of the shell to advance beyond its current sequence of steps. Designed for functions; as if called from the main body of the script, it causes the script to exit. |
| `set` | Used to determine the value of environmental variables of the current shell and its descendants. |
| `shift` | Used to traverse a shell's argument list or a list of field-separated words. |
| `stop` | Stops a specified job. |
| `suspend` | Halts the current shell. |
| `test` | Synonymous with square brackets `[...]`; evaluates a condition, and if the condition is true, executes an action. |
| `times` | Prints the total user and system times for processes running from the shell. |
| `trap` | Responds to hardware signals. |
| `type` | Writes a description of a command type. |
| `typeset` | Sets or gets attributes and values for shell variables and functions. |
| `ulimit` | Sets or gets limitations on the system resources available to the current shell and its descendants. |
| `umask` | Sets or gets the file mode creation mask. |
| `unset` | Changes an environmental variable for the current shell and its descendants back to the default. |
| `until` | Repetitively executes a series of actions. |
| `wait` | Used to await process completion until conditions are evaluated to true. |
| `while` | Repetitively executes a series of commands while conditions are evaluated as true. |

![](img/256e02a6afce528d264a8d911fa0ff20_719_0.png)

When using control structures, you must supply at least one argument or your output will be garbled. The test utility will check to see that you have at least one argument in a script. It may also ask a question about the status of a file argument, and it will test the argument to see if it is the name of a regular file and not a directory. The test utility has several options that may be used to test the characteristics of a file. They are listed in Table 18.2.

### TABLE 18.2: TEST UTILITY OPTIONS

| **Option** | **Test** |
|---|---|
| -d | Existing directory file |
| -f | Existing regular file |
| -r | Existing readable file |
| -s | Existing file with length greater than 0 |
| -w | Existing writable file |
| -x | Existing executable file |

Use the options to test arguments as in the following example:

```bash
$ cat checker
#!/bin/sh
# checker - checks to see if there are arguments to checker
if [ $# -gt 0 ]
then
    echo "You put $# arguments on my command line."
    exit 1
fi
echo "You did not put any arguments on my command line."
```
