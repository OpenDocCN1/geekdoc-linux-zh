
## Using multiple variables

The C-style `for` command also allows you to use multiple variables for the iteration. The loop handles each variable separately, allowing you to define a different iteration process for each variable. Although you can have multiple variables, you can define only one condition in the `for` loop:

```bash
$ cat test9
#!/bin/bash
# multiple variables

for (( a=1, b=10; a <= 10; a++, b-- ))
do
   echo "$a - $b"
done
$ ./test9
1 - 10
2 - 9
3 - 8
4 - 7
5 - 6
6 - 5
7 - 4
8 - 3
9 - 2
10 - 1
$
```

The `a` and `b` variables are each initialized with different values, and different iteration processes are defined. While the loop increases the `a` variable, it decreases the `b` variable for each iteration.

## Exploring the `while` Command

The `while` command is somewhat of a cross between the `if-then` statement and the `for` loop. The `while` command allows you to define a command to test and then loop through a set of commands for as long as the defined test command returns a 0 exit status. It tests the test command at the start of each iteration. When the test command returns a non-0 exit status, the while command stops executing the set of commands.

### Understanding the basic while format

Here's the format of the while command:

```bash
while test_command
do
    other_commands
done
```

The `test_command` defined in the while command is the exact same format as used in if-then statements (see Chapter 11). As in the if-then statement, you can use any normal Bash shell command, or you can use the `test_command` to test for conditions, such as variable values.

The key to the while command is that the exit status of the `test_command` specified must change, based on the commands run during the loop. If the exit status never changes, the while loop will get stuck in an infinite loop.

The most common use of the `test_command` is to use brackets to check a value of a shell variable that's used in the loop commands:

```bash
$ cat test10
#!/bin/bash
# while command test

vari=10
while [ $vari -gt 0 ]
do
    echo $vari
    vari=$[ $vari - 1 ]
done
$ ./test10
10
9
8
7
6
5
4
3
2
1
$
```

The while command defines the test condition to check for each iteration:

```bash
while [ $vari -gt 0 ]
```

![](img/0798d50a0e5dbf1265fbda3832b3e015_338_0.png)

As long as the test condition is true, the `while` command continues to loop through the commands defined. Within the commands, the variable used in the test condition must be modified, or you'll have an infinite loop. This example uses shell arithmetic to decrease the variable value by 1:

```bash
var1=$[ $var1 - 1 ]
```

The `while` loop stops when the test condition is no longer true.

### Using multiple test commands

The `while` command allows you to define multiple test commands on the `while` statement line. Only the exit status of the last test command is used to determine when the loop stops. This can cause some interesting results if you're not careful. Here's an example:

```bash
$ cat test11
#!/bin/bash
# testing a multicommand while loop

var1=10

while echo $var1
    [ $var1 -ge 0 ]
do
    echo "This is inside the loop"
    var1=$[ $var1 - 1 ]
done
$ ./test11
10
This is inside the loop
9
This is inside the loop
8
This is inside the loop
7
This is inside the loop
6
This is inside the loop
5
This is inside the loop
4
This is inside the loop
3
This is inside the loop
2
This is inside the loop
1
This is inside the loop
0
This is inside the loop
-1
$
```

Pay close attention to what happened in this example. Two test commands were defined in the while statement:

```bash
while echo $var1
    [ $var1 -ge 0 ]
```

The first test simply displays the current value of the `var1` variable. The second test uses brackets to determine the value of the `var1` variable. Inside the loop, an echo statement displays a simple message, indicating that the loop was processed. Notice when you run the example how the output ends:

```bash
This is inside the loop
-1
$
```

The while loop executed the echo statement when the `var1` variable was equal to 0 and then decreased the `var1` variable value. The test commands were then executed for the next iteration. The echo test command was executed, displaying the value of the `var1` variable, which is now less than 0. It’s not until the shell executes the test command that the while loop terminates.

This demonstrates that in a multicommand while statement, all the test commands are executed in each iteration, including the last iteration when the last test command fails. Be careful of this. Another thing to be careful of is how you specify the multiple test commands. Note that each test command is on a separate line!

## Using the until Command

The `until` command works in exactly the opposite way from the `while` command. The `until` command requires that you specify a test command that normally produces a non-0 exit status. As long as the exit status of the test command is non-0, the Bash shell executes the commands listed in the loop. When the test command returns a 0 exit status, the loop stops.

As you would expect, the format of the `until` command is:

```bash
until test commands
do
    other commands
done
```

Similar to the while command, you can have more than one test command in the `until` command statement. Only the exit status of the last command determines if the Bash shell executes the other commands defined.

The following is an example of using the `until` command:

```bash
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

This example tests the `var1` variable to determine when the `until` loop should stop. As soon as the value of the variable is equal to 0, the `until` command stops the loop. The same caution I warned you about for the `while` command applies when you use multiple test commands with the `until` command:

```bash
$ cat test13
#!/bin/bash
# using the until command

var1=100

until echo $var1
    [ $var1 -eq 0 ]
do
    echo Inside the loop: $var1
    var1=$[ $var1 - 25 ]
done
$ ./test13
100
Inside the loop: 100
75
Inside the loop: 75
50
Inside the loop: 50
25
Inside the loop: 25
0
$
```

The shell executes the test commands specified and stops only when the last command is true.

## Nesting Loops

A loop statement can use any other type of command within the loop, including other loop commands. This is called a *nested loop*. Take care when you use nested loops, because you're performing an iteration within an iteration, which multiplies the number of times commands are being run. If you don't pay close attention to this, it can cause problems in your scripts.

Here's a simple example of nesting a `for` loop inside another `for` loop:

```bash
$ cat test14
#!/bin/bash
# nesting for loops

for ( ( a = 1; a <= 3; a++ ))
do
    echo "Starting loop: $a"
    for ( ( b = 1; b <= 3; b++ ))
    do
        echo "  Inside loop: $b"
    done
done
$ ./test14
Starting loop 1:
  Inside loop: 1
  Inside loop: 2
  Inside loop: 3
Starting loop 2:
  Inside loop: 1
  Inside loop: 2
  Inside loop: 3
Starting loop 3:
  Inside loop: 1
  Inside loop: 2
  Inside loop: 3
$
```

The nested loop (also called the inner loop) iterates through its values for each iteration of the outer loop. Notice that there's no difference between the `do` and `done` commands for the two loops. The Bash shell knows that when the first `done` command is executed, it refers to the inner loop and not the outer loop.

The same applies when you mix loop commands, such as placing a `for` loop inside a `while` loop:

```bash
$ cat test15
#!/bin/bash
# placing a for loop inside a while loop

var1=5

while [ $var1 -ge 0 ]
do
    echo "Outer loop: $var1"
    for ( ( var2 = 1; $var2 < 3; var2++ ))
    do
        var3=$[ $var1 * $var2 ]
        echo "  Inner loop: $var1 * $var2 = $var3"
    done
    var1=$[ $var1 - 1 ]
```
