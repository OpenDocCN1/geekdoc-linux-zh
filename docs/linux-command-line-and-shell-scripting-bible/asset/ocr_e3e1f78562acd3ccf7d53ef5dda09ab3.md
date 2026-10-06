# Part II Shell Scripting Basics

Values are assigned to user variables using an equal sign. No spaces can appear between the variable, the equal sign, and the value (another trouble spot for novices). Here are a few examples of assigning values to user variables:

```
var1=10
var2=-57
var3=testing
var4="still more testing"
```

The shell script automatically determines the data type used for the variable value. Variables defined within the shell script maintain their values throughout the life of the shell script but are deleted when the shell script completes.

Just like system variables, user variables can be referenced using the dollar sign:

```
$ cat test3
!/bin/bash
# testing variables
days=10
guest="Katie"
echo "$guest checked in $days days ago"
days=5
guest="Jessica"
echo "$guest checked in $days days ago"
$
```

Running the script produces the output:

```
$ chmod u+x test3
./test3
Katie checked in 10 days ago
Jessica checked in 5 days ago
$
```

Each time the variable is referenced, it produces the value currently assigned to it. It is important to remember that when referencing a variable you use the dollar sign, but when referencing the variable to assign a value to, you do not use the dollar sign. Here's an example of what I mean:

```
$ cat test4
!/bin/bash
# assigning a variable value to another variable
```

```
value1=10
value2=$value
echo The resulting value is $value2
$
```