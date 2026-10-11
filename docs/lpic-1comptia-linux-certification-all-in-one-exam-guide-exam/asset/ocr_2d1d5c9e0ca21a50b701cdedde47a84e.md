It is very common to use the `seq` command within a `for` loop to create the sequence of numbers to determine how many times it will loop. There are three options for creating a number sequence with `seq`:

+   *   If you specify a single value, the sequence starts at one, increments by one, and ends at the specified value.
+   *   If you specify two values, the sequence starts at the first value, increments by one, and ends at the second value.
+   *   If you specify three values, the sequence starts at the first value, increments by the second value, and ends at the third value.

Consider the following example:

```
seq 5 15
```

This command creates a sequence of numbers that starts at 5, increments by 1, and ends at 15. Here is an example of using `seq` in a `for` loop:

```
for i in `seq 15`
do
    echo "The current number in the sequence is $i."
done
exit 0
```

The biggest danger with looping structures is that it is possible to get stuck in an infinite loop. This happens when the condition never changes to a value that will break the loop. In this situation, the script gets "hung" because it keeps running the same loop structure over and over and over and will continue to do so until you manually break out of it using the **CTRL-C** key.

Let's practice working with basic shell scripts in the following exercise.

# Exercise 14-1: Creating a Basic Shell Script

![](bbox=[0.17, 0.68, 0.25, 0.725])

> **VIDEO** For more information watch *Exercise 14-1*.

In this exercise, you will practice creating a basic shell script. This script will ask the user for a series of three numbers. It will then ask the user if he or she wants to sum the three numbers or average them. You will also add the execute permission to the file to allow the file owner to run it. Complete the following:

+   1.  If necessary, boot your Linux system and log in as a standard user.
+   2.  Change to the `~/bin` directory.
+   3.  At the shell prompt enter `vi domath`.
+   4.  Enter the following script:

```
#!/bin/bash
#A script to do some simple math.
clear
declare -i A
```