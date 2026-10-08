A run of the `lpmnum` script with multiple arguments is shown here:

```
$ lpmnum mydata pref ace
```

# # Control Structures

You can control the execution of Linux commands in a shell script with control structures.
Control structures allow you to repeat commands and to select certain commands over others.
A control structure consists of two major components: a test and commands. If the test is
successful, then the commands are executed. In this way, you can use control structures to
make decisions as to whether commands should be executed.

There are two different kinds of control structures: **loops** and **conditions**. A loop repeats
commands, whereas a condition executes a command when certain conditions are met. The
BASH shell has three loop control structures: **while**, **for**, and **for-in**. There are two
condition structures: **if** and **case**. The control structures have as their test the execution of
a Linux command. All Linux commands return an exit status after they have finished
executing. If a command is successful, its exit status will be 0. If the command fails for any
reason, its exit status will be a positive value referencing the type of failure that occurred.
The control structures check to see if the exit status of a Linux command is 0 or some other
value. In the case of the **if** and **while** structures, if the exit status is a zero value, then the
command was successful and the structure continues.

# ## Test Operations

With the **test** command, you can compare integers, compare strings, and even perform
logical operations. The command consists of the keyword **test** followed by the values
being compared, separated by an option that specifies what kind of comparison is taking
place. The option can be thought of as the operator, but it is written, like other options, with
a minus sign and letter codes. For example, **-eq** is the option that represents the equality
comparison. However, there are two string operations that actually use an operator instead
of an option. When you compare two strings for equality, you use the equal sign (=). For
inequality you use !=. Table 8-8 lists some of the commonly used options and operators
used by **test**. The syntax for the **test** command is shown here:

```
test value -option value
test string = string
```

In the next example, the user compares two integer values to see if they are equal. In
this case, you need to use the equality option, **-eq**. The exit status of the **test** command is
examined to find out the result of the test operation. The shell special variable `$?` holds the
exit status of the most recently executed Linux command.

```
$ num=5
$ test $num -eq 10
$ echo $?
1
```