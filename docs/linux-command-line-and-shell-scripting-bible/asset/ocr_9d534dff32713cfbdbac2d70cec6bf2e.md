Each command has a different use in how to control the operation of a loop. The following sections describe how you can use these commands to control the operation of your loops.

# The break command

The break command is a simple way to escape out of a loop in progress. You can use the break command to exit out of any type of loop, including while and until loops.

There are several situations in which you can use the break command. This section shows each of these methods.

# Breaking out of a single loop

When the shell executes a break command, it attempts to break out of the loop that's currently processing:

```
$ cat test17
!/bin/bash
# breaking out of a for loop

for var in 1 2 3 4 5 6 7 8 9 10
do
if [ $var -eq 5 ];
then
break
fi
echo "Iteration number: $var"
done
echo "The loop is completed"
$ ./test17
Iteration number: 1
Iteration number: 2
Iteration number: 3
Iteration number: 4
The loop is completed
$ 
```

The loop should normally have iterated through all of the values specified in the list. However, if the if-then condition was satisfied, the shell executed the break command, which stopped the for loop.

This technique also works for while and until loops:

```
$ cat test18
!/bin/bash
# breaking out of a while loop

var=1

while [ $var -lt 10 ]
do
```