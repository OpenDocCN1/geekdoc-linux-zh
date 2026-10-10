# **Part II: Shell Scripting Basics**

```
```
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

This example tests the `var1` variable to determine when the `until` loop should stop. As soon as the value of the variable is equal to 0, the `until` command stops the loop. The same caution I warned you about for the `while` command applies when you use multiple test commands with the `until` command:

```
```
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
```

The shell executes the test commands specified and stops only when the last command is true.

# **Nesting Loops**

A loop statement can use any other type of command within the loop, including other loop commands. This is called a *nested loop*. Take care when you use nested loops, because you're performing an iteration within an iteration, which multiplies the number of times commands are being run. If you don't pay close attention to this, it can cause problems in your scripts.