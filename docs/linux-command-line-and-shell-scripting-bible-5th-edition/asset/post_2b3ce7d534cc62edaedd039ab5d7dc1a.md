
# Part II: Shell Scripting Basics

done
$ ./test15
Outer loop: 5
    Inner loop: 5 * 1 = 5
    Inner loop: 5 * 2 = 10
Outer loop: 4
    Inner loop: 4 * 1 = 4
    Inner loop: 4 * 2 = 8
Outer loop: 3
    Inner loop: 3 * 1 = 3
    Inner loop: 3 * 2 = 6
Outer loop: 2
    Inner loop: 2 * 1 = 2
    Inner loop: 2 * 2 = 4
Outer loop: 1
    Inner loop: 1 * 1 = 1
    Inner loop: 1 * 2 = 2
Outer loop: 0
    Inner loop: 0 * 1 = 0
    Inner loop: 0 * 2 = 0
$

Again, the shell distinguished between the `do` and `done` commands of the inner `for` loop from the same commands in the outer `while` loop.

If you really want to test your brain, you can *even* combine `until` and `while` loops:

```bash
$ cat test16
#!/bin/bash
# using until and while loops

var1=3

until [ $var1 -eq 0 ]
do
    echo "Outer loop: $var1"
    var2=1
    while [ $var2 -lt 5 ]
    do
        var3=$(echo "scale=4; $var1 / $var2" | bc)
        echo "    Inner loop: $var1 / $var2 = $var3"
        var2=$[ $var2 + 1 ]
    done
    var1=$[ $var1 - 1 ]
done
$ ./test16
Outer loop: 3
    Inner loop: 3 / 1 = 3.0000
    Inner loop: 3 / 2 = 1.5000
    Inner loop: 3 / 3 = 1.0000
    Inner loop: 3 / 4 = .7500
Outer loop: 2
    Inner loop: 2 / 1 = 2.0000
    Inner loop: 2 / 2 = 1.0000
    Inner loop: 2 / 3 = .6666
    Inner loop: 2 / 4 = .5000
Outer loop: 1
    Inner loop: 1 / 1 = 1.0000
    Inner loop: 1 / 2 = .5000
    Inner loop: 1 / 3 = .3333
    Inner loop: 1 / 4 = .2500
$
```

The outer until loop starts with a value of 3 and continues until the value equals 0. The inner while loop starts with a value of 1 and continues as long as the value is less than 5. Each loop must change the value used in the test condition, or the loop will get stuck infinitely.

## Looping on File Data

Often, you must iterate through items stored inside a file. This requires combining two of the techniques covered:

-   Using nested loops
-   Changing the *IFS* environment variable

By changing the *IFS* environment variable, you can force the for command to handle each line in the file as a separate item for processing, even if the data contains spaces. After you've extracted an individual line in the file, you may have to loop again to extract data contained within it.

The classic example of this is processing data in the /etc/passwd file. This requires that you iterate through the /etc/passwd file line by line and then change the IFS variable value to a colon so that you can separate the individual components in each line.

The following is an example of doing just that:

```bash
#!/bin/bash
# changing the IFS value

IFS.OLD=$IFS
IFS=$' \n'
for entry in $(cat /etc/passwd)
do
    echo "Values in $entry --"
    IFS=:
    for value in $entry
    do
        echo "     $value"
    done
done
$
```

This script uses two different `IFS` values to parse the data. The first `IFS` value parses the individual lines in the `/etc/passwd` file. The inner `for` loop next changes the `IFS` value to the colon, which allows you to parse the individual values within the `/etc/passwd` lines.

When you run this script, you get something like this:

```text
Values in rich:x:501:501:Rich Blum:/home/rich:/bin/bash --
rich
x
501
501
Rich Blum
/home/rich
/bin/bash

Values in katie:x:502:502:Katie Blum:/home/katie:/bin/bash --
katie
x
502
502
Katie Blum
/home/katie
/bin/bash
```

The inner `loop` parses each individual value in the `/etc/passwd` entry. This is also a great way to process comma-separated data, which is often how spreadsheet data is imported.

## Controlling the Loop

You might be tempted to think that after you start a loop, you’re stuck until the loop finishes all its iterations. This is not true. A couple of commands help control what happens inside a loop:

-   The `break` command
-   The `continue` command

Each command has a different use in controlling the operation of a loop. The following sections describe how you can use these commands to control the operation of your loops.

### The `break` command

The `break` command is a simple way to escape a loop in progress. You can use the `break` command to exit any type of loop, including `while` and `until` loops.

You can use the `break` command in several situations. This section shows each of these methods.

#### Breaking out of a single loop

When the shell executes a `break` command, it attempts to break out of the loop that’s currently processing:

```bash
$ cat test17
#!/bin/bash
# breaking out of a for loop

for var1 in 1 2 3 4 5 6 7 8 9 10
do
    if [ $var1 -eq 5 ]
    then
        break
    fi
    echo "Iteration number: $var1"
done
echo "The for loop is completed"
$ ./test17
Iteration number: 1
Iteration number: 2
Iteration number: 3
Iteration number: 4
The for loop is completed
$
```

The `for` loop should normally have iterated through all the values specified in the list. However, when the `if-then` condition was satisfied, the shell executed the `break` command, which stopped the `for` loop.

This technique also works for `while` and `until` loops:

```bash
$ cat test18
#!/bin/bash
# breaking out of a while loop

var1=1

while [ $var1 -lt 10 ]
do
    if [ $var1 -eq 5 ]
    then
        break
    fi
    echo "Iteration: $var1"
    var1=$[ $var1 + 1 ]
done

echo "The while loop is completed"
$ ./test18
Iteration: 1
Iteration: 2
Iteration: 3
Iteration: 4
The while loop is completed
$
```

The `while` loop terminated when the `if-then` condition was met, executing the `break` command.

#### Breaking out of an inner loop

When you're working with multiple loops, the `break` command automatically terminates the innermost loop you're in:

```bash
$ cat test19
#!/bin/bash
# breaking out of an inner loop

for( ( a = 1; a < 4; a++ ))
do
    echo "Outer loop: $a"
    for( ( b = 1; b < 100; b++ ))
    do
        if [ $b -eq 5 ]
        then
            break
        fi
        echo "    Inner loop: $b"
    done
done
$ ./test19
Outer loop: 1
    Inner loop: 1
    Inner loop: 2
    Inner loop: 3
    Inner loop: 4
Outer loop: 2
    Inner loop: 1
    Inner loop: 2
    Inner loop: 3
    Inner loop: 4
Outer loop: 3
    Inner loop: 1
    Inner loop: 2
    Inner loop: 3
    Inner loop: 4
$
```

The `for` statement in the inner loop specifies to iterate until the `b` variable is equal to `100`. However, the `if-then` statement in the inner loop specifies that when the `b` variable value is equal to `5`, the `break` command is executed. Notice that even though the inner loop is terminated with the `break` command, the outer loop continues working as specified.

#### Breaking out of an outer loop

There may be times when you're in an inner loop but need to stop the outer loop. The `break` command includes a single command-line parameter value:

```bash
break n
```

where $n$ indicates the level of the loop to break out of. By default, $n$ is $1$, indicating to break out of the current loop. If you set $n$ to a value of $2$, the `break` command stops the next level of the outer loop:

```bash
$ cat test20
#!/bin/bash
# breaking out of an outer loop
for (( a = 1; a < 4; a++ ))
do
    echo "Outer loop: $a"
    for (( b = 1; b < 10; b++ ))
    do
        if [ $b -gt 4 ]
        then
            break 2
        fi
        echo "  Inner loop: $b"
    done
done
$ ./test20
Outer loop: 1
  Inner loop: 1
  Inner loop: 2
  Inner loop: 3
  Inner loop: 4
$
```

Now when the shell executes the `break` command, the outer loop stops.

## The continue command

The `continue` command is a way to prematurely stop processing commands inside a loop but not terminate the loop completely. This allows you to set conditions within a loop where the shell won't execute commands. Here's a simple example of using the `continue` command in a for loop:

```bash
$ cat test21
#!/bin/bash
# using the continue command
for (( var1 = 1; var1 < 15; var1++ ))
do
    if [ $var1 -gt 5 ] && [ $var1 -lt 10 ]
    then
        continue
    fi
    echo "Iteration number: $var1"
done
$ ./test21
```
