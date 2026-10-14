# Part 5: Programming in Ubuntu

The shell script automatically determines the data type used for the variable value. Variables defined within the shell script maintain their values throughout the life of the shell script, but are deleted when the shell script completes.

Just like system variables, user variables can be referenced using the dollar sign:

```
```bash
$cat test3
#!/bin/bash
# testing variables
days=10
guest="Katie"
echo "$guest checked in $days days ago"
days=5
guest="Jessica"
echo "$guest checked in $days days ago"
Running the script produces the output:
$ ./test3
Katie checked in 10 days ago
Jessica checked in 5 days ago
$
```
```

Each time the variable is referenced, it produces the value currently assigned to it. It’s important to remember that when referencing a variable value, you use the dollar sign, but when referencing the variable to assign a value to it, you do not use the dollar sign. Here’s an example of what I mean:

```
```bash
#!/bin/bash
# assigning a variable value to another variable

value1=10
value2=$value1
echo The resulting value is $value2
```
```

When you use the value of the value1 variable in the assignment statement, you must still use the dollar sign. This code produces the output:

```
```bash
$ ./test4
The resulting value is 10
$
```
```

If you forget the dollar sign, and make the value2 assignment line look like:

```
```bash
value2=value1
```
```

you get the following output:

```
```bash
$ ./test4
The resulting value is value1
$
```
```

Without the dollar sign the shell interprets the variable name as a normal text string, which is probably not what you wanted.