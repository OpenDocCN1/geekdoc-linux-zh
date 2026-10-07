# 288  Lab 6.1: Typed Variables and Scope

LAB
6.1

use the print command. Instead of print, you can use the printf command, which is covered in Lab 11.1. Here is a printf command that shows the result of an arithmetic expansion, print with three digits to the right of the decimal point:

```
printf "%.3f\n" $(( sqrt(2)) ))
1.414
```

# 6.1.4 ANSWERS

Prepare the following script, and put it in the file ~/fun/f614
Now run the following sequence of commands:

+   unset y z
float z=3.14159
~/fun/f614
print x=$x y=$y z=$z
f614_ksh
print x=$x y=$y z=$z
f614_posix
print x=$x y=$y z=$z

+   What does the unset command accomplish?

Answer: It makes sure that the three variables do not have types set for them from earlier commands you may have run.

In particular, it is important that x and y must not have types or values, because that would make it difficult to evaluate the effects of running this particular script.

+   What does the dot command accomplish?

Answer: It runs the script in the context of the current shell, as described in Chapter I, "Setting Up.".

When you do this script, the assignment commands to the variables x and y are executed, the shell memorizes the function definitions, but it does not execute the functions.

+   What is the effect of running f614_ksh on the value of x?

Answer:Your interaction should look like the following: