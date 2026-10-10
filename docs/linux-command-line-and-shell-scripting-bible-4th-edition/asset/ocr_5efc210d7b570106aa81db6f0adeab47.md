# **Using the until Command**

The `until` command works in exactly the opposite way from the `while` command. The `until` command requires that you specify a test command that normally produces a non-zero exit status. As long as the exit status of the test command is non-zero, the Bash shell executes the commands listed in the loop. When the test command returns a zero exit status, the loop stops.

As you would expect, the format of the `until` command is

```
```
until test commands
do
    other commands
done
```
```

Similar to the `while` command, you can have more than one test command in the `until` command statement. Only the exit status of the last command determines if the Bash shell executes the *other commands* defined.

The following is an example of using the `until` command:

```
```
$ cat test12
#!/bin/bash
# using the until command

var1=100

until [ $var1 -eq 0 ]
do
    echo $var1
    var1=$[ $var1 - 25 ]
done
$ ./test12
100
75
50
25
$ 
```
```

This example tests the `var1` variable to determine when the `until` loop should stop. As soon as the value of the variable is equal to 0, the `until`