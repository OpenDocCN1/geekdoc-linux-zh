# Using Loops

If you had a list of one thousand names and your job was to assign an account for all the names on the list, this would get tedious in a hurry. So what's the solution? Loops! A loop is a structure in a script or program that allows conditional repeating of code. The structures supported by the bash scripting language are for, while, and until. Each structure has a different purpose.

# The for Loop

A `for` loop lets you execute a specific group of script statements a set number of times. The bash script for is a little different from that in other programming languages in that it lets you iterate a series of words within a string.

Consider the following for loop example.

```
```
for I in $(ls); do
    echo "$item;" $I
done
```
```

This for loop uses the variable `I` to contain each value of the list provided. The list provided is identified after the `in` statement and is a command to list the directory, `$(ls)`. The variable takes on the value of each value in the list and the next line, `echo "$item;" $I`, prints each filename in the directory.

For loops can be very useful. Take the "days in a month" case example from The case Statement section earlier in this chapter and use a for loop instead of a command-line argument to provide a value for the case. For example:

```
```bash
#!/bin/bash

for MONTH in January February March April May June July August September October November December;
do
    case $MONTH in
        January|March|May|July|August|October|December)
            echo "$MONTH has 31 days;;
        April|June|September|November)
            echo "$MONTH has 30 days;;
        February)
            let VAL1=$(date +%Y)%4
            if [ $VAL1 -eq 0 ]; then
                echo "$MONTH has 29 days
            else
                echo "$MONTH has 28 days
            fi;;
    esac
done
```
```

This is a case statement inside a for loop. Based on the value of `MONTH`, different numbers of days will be displayed on the screen. The resulting output would be:

```
```
January has 31 days
February has 28 days
March has 31 days
April has 30 days
May has 31 days
June has 30 days
July has 31 days
```
```