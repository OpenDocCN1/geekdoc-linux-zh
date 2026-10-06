# Shell Scripting Basics

```
if [ $varl -eq 5 ]
then
    break
fi
echo "Iteration: $varl"
varl=$[$varl + 1]
done
echo "The while loop is completed"
$./test18
Iteration: 1
Iteration: 2
Iteration: 3
Iteration: 4
The while loop is completed
$
```

The while loop terminated when the if-then condition was met, executing the break command.

# Breaking out of an inner loop

When you're working with multiple loops, the break command automatically terminates the innermost loop you're:

```
$ cat test19
#!/bin/bash
# breaking out of an inner loop

for (( a = 1; a < 4; a++ ))
do
    echo "Outer loop: $a"
    for (( b = 1; b < 100; b++ ))
    do
        if [ $b -eq 5 ]
        then
            break
        fi
        echo "Inner loop: $b"
    end
done
$./test19
Outer loop: 1
Inner loop: 1
Inner loop: 2
Inner loop: 3
Inner loop: 4
Outer loop: 2
Inner loop: 1
Inner loop: 2
```