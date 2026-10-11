
This is 18 in the while loop.

The loop continues to the final line:

This is 1 in the while loop.

## Multiple Test Commands

You can pack up multiple test commands in the while loop.

```bash
$ cat test1133
#!/bin/bash
# Now I am testing a multicommand while loop in Linux shell
var15=20
while echo $var15
[ $var15 -ge 0 ]
do
  echo "This operation is being conducted inside the while loop."
  var15=$[ $var15 - 1 ]
done
```

```bash
$ bash -f main.sh
20
This operation is being conducted inside the while loop.
19
This operation is being conducted inside the while loop.
18
This operation is being conducted inside the while loop.
17
This will continue until it reaches the last number:
This operation is being conducted inside the while loop.
0
This operation is being conducted inside the while loop.
-1
```

The first test command displays the present value of var15 variable. The second command will use the test command to know the value of var15 variable. The echo statement returns a simple message within the loop that indicates that the loop has run its course.

### The until Command

The until command works opposite to the while command. It requires a simple test command is specified, which will produce a non-zero exit status, at which point the bash shell will execute the while loop commands.

However, similar to the while command, the until command statement can also contain multiple test commands, and the exit status of the final command is the determining factor.

```bash
$ cat test1222
#!/bin/bash
# In this code block I will be using the until command
var15=100
until [ $var15 -eq 0 ]
do
    echo You are seeing the operations of the until command. The next digit in the loop is $var15
    var15=$[ $var15 - 5 ]
done
```

```bash
$ bash -f main.sh
You are seeing the operations of the until command. The next digit in the loop is 100

You are seeing the operations of the until command. The next digit in the loop is 95

You are seeing the operations of the until command. The next digit in the loop is 90

And continuing, until it reaches the final digit:

You are seeing the operations of the until command. The next digit in the loop is 5
```

The example has successfully tested the var15 variable in order to determine when the loop will stop - when the value of the variable drops down to zero, the until command stops right away.

```bash
$ cat test1222
#!/bin/bash
# In this code block, I will be using the until command
var15=100
until echo $var15
    [ $var15 -eq 0 ]
do
    echo You are seeing the operations of the until command. The next digit in the loop is $var15
    var15=$[ $var15 - 5 ]
done
```

```bash
$ bash -f main.sh
100
You are seeing the operations of the until command. The next digit in the loop is 100

95
You are seeing the operations of the until command. The next digit in the loop is 95

90
Again, this will continue to the last digit in the loop:

You are seeing the operations of the until command. The next digit in the loop is 5

0
```

## Nesting Loops

A loop statement may use another command inside of the loop, including other commands of the same loop. The process is known as nested looping. You will have an iteration inside another iteration, which will multiply the number of times a command is being run. See an example to get a grasp of how you can nest loops.

```bash
$ cat test1444
#!/bin/bash
# The following code block shows nesting for loops
for (( x = 1; x <= 7; x++ ))
do
    echo "You are seeing the operations of the until command. The next digit in the loop is $x:"
    for (( y = 1; y <= 7; y++ ))
    do
        echo " Now you are seeing what is going on inside loop: $y"
    done
done
```

```bash
$ bash -f main.sh
You are seeing the operations of the until command. The next digit in the loop is 1:

Now you are seeing what is going on inside loop: 1

Now you are seeing what is going on inside loop: 2

And so on, finishing with

Now you are seeing what is going on inside loop: 7

You are seeing the operations of the until command. The next digit in the loop is 2:

Now you are seeing what is going on inside loop: 1

Now you are seeing what is going on inside loop: 2

Again, this will continue until it ends with

Now you are seeing what is going on inside loop: 7

You are seeing the operations of the until command. The next digit in the loop is 3:

Now you are seeing what is going on inside loop: 1

Now you are seeing what is going on inside loop: 2

Ending with:

Now you are seeing what is going on inside loop: 7

You are seeing the operations of the until command. The next digit in the loop is 4:

Now you are seeing what is going on inside loop: 1

Now you are seeing what is going on inside loop: 2

Ending with:

Now you are seeing what is going on inside loop: 7

The entire cycle continues through the loop, until it reaches:

Now you are seeing what is going on inside loop: 7
```

You can experiment with the numbers in the loop to contract or expand the two loops' sizes. By changing the numbers of the loops, you will be able to change how the loop will behave.

```bash
$ cat test1444
#!/bin/bash
# The following code block shows nesting for loops
for (( x = 1; x <= 3; x++ ))
do
    echo "You are seeing the operations of the until command. The next digit in the loop is $x:"
    for (( y = 1; y <= 5; y++ ))
    do
        echo " Now you are seeing what is going on inside loop: $y"
    done
done
```

```bash
$ bash -f main.sh
You are seeing the operations of the until command. The next digit in the loop is 1:

Now you are seeing what is going on inside loop: 1

Repeated to:

Now you are seeing what is going on inside loop: 5

You are seeing the operations of the until command. The next digit in the loop is 2:

Now you are seeing what is going on inside loop: 1

Repeated to:

Now you are seeing what is going on inside loop: 5

You are seeing the operations of the until command. The next digit in the loop is 3:

Now you are seeing what is going on inside loop: 1

And finishing on:

Now you are seeing what is going on inside loop: 5
```

The nested loop iterates through the values for iterations of the outer loop. There is no difference between the do and done commands for two loops. You can create a nested loop by pairing up for loops and while loops.

```bash
$ cat test15
#!/bin/bash
# This is how we can place a for loop in a while loop
var15=15
while [ $var15 -ge 0 ]
do
    echo "You are seeing the operations of nesting loops. The next digit in the loop is $var15:"
    for (( var12 = 1; var12 < 3; var12++ ))
    do
        var13=$[ $var15 * $var12 ]
        echo " Now you are seeing what is going on inside loop: $var15 * $var12 = $var13"
    done
    var15=$[ $var15 - 1 ]
done
```

```bash
$ bash -f main.sh
You are seeing the operations of nesting loops. The next digit in the loop is 15:

Now you are seeing what is going on inside loop: 15 * 1 = 15

Now you are seeing what is going on inside loop: 15 * 2 = 30

This will continue down to the final line:

You are seeing the operations of nesting loops. The next digit in the loop is 0:

Now you are seeing what is going on inside loop: 0 * 1 = 0

Now you are seeing what is going on inside loop: 0 * 2 = 0
```

In the next example, I will pair up until and while loops to test nesting loops' limits. See the following example.

```bash
$ cat test16
#!/bin/bash
var15=10
until [ $var15 -eq 0 ]
do
    echo "You are seeing the operations of the nested until and while loops: $var15"
    var12=1
    while [ $var12 -lt 5 ]
    do
        var13=$(echo "scale=4; $var15 / $var12" | bc)
        echo " This is how the inner section of the nested loop functions: $var15 / $var12 = $var13"
        var12=$[ $var12 + 1 ]
    done
    var15=$[ $var15 - 1 ]
done
```

```bash
$ bash -f main.sh
You are seeing the operations of the nested until and while loops: 10

This is how the inner section of the nested loop functions: 10 / 1 = 10.0000

This is how the inner section of the nested loop functions: 10 / 2 = 5.0000

This is how the inner section of the nested loop functions: 10 / 3 = 3.3333

This is how the inner section of the nested loop functions: 10 / 4 = 2.5000

This cycle is repeated, until it reaches the final one of:

You are seeing the operations of the nested until and while loops: 1

This is how the inner section of the nested loop functions: 1 / 1 = 1.0000

This is how the inner section of the nested loop functions: 1 / 2 = .5000

This is how the inner section of the nested loop functions: 1 / 3 = .3333

This is how the inner section of the nested loop functions: 1 / 4 = .2500
```

## Loop Control

You might think that once a loop starts, you will be stuck in that until the loop has run its course. However, there is a way out. You can add to the code a couple of commands that help you control the inside of the loop.

The break command is the simplest way to move out of a loop that is in progress. You may use the break command to exit while and until loops.

```bash
$ cat test17
#!/bin/bash
for countries in 2 3 4 5 6 7 8 9 10 11 12 13 14
do
    if [ $countries -eq 12 ]
    then
        break
    fi
    echo "I am going to visit $countries after Covid-19 is over."
done
echo "I have visited all the countries."
```

```bash
$ bash -f main.sh
I am going to visit 2 countries after Covid-19 is over.

I am going to visit 3 countries after Covid-19 is over.

I am going to visit 4 countries after Covid-19 is over.
```
