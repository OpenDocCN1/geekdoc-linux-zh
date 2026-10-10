You supply the series of values used in the iterations in the `list` parameter. You can specify the values in the list in several ways.

In each iteration, the `var` variable contains the current value in the list. The first iteration uses the first item in the list, the second iteration the second item, and so on, until all the items in the list have been used.

The commands entered between the `do` and `done` statements can be one or more standard Bash shell commands. Within the commands, the `$var` variable contains the value of the current list item for the iteration.

> **NOTE**
> If you prefer, you can include the do statement on the same line as the for statement, but you must separate it from the list items using a semicolon: for var in list; do.

I mentioned that there are several ways to specify the values in the list. The following sections show the various ways.

# Reading values in a list

The most basic use of the `for` command is to iterate through a list of values defined within the `for` command itself:

```
```
$ cat test1
#!/bin/bash
# basic for command

for test in Alabama Alaska Arizona Arkansas California Colorado
do
    echo The next state is $test
done
$ ./test1
The next state is Alabama
The next state is Alaska
The next state is Arizona
The next state is Arkansas
The next state is California
The next state is Colorado
$
```
```

Each time the `for` command iterates through the list of values provided, it assigns the `$test` variable the next value in the list. The `$test` variable can be used just like any other script variable within the `for` command statements. After the last iteration, the `$test` variable remains valid throughout the remainder of the shell script. It retains the last iteration value (unless you change its value):