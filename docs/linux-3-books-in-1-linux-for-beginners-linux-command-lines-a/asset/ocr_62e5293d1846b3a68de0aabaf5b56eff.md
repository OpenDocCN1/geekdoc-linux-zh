```
$ cat test1222
#!/bin/bash
# In this code block I will be using the until command
var15=100
until [ $var15 -eq 0 ]
do
echo You are seeing the operations of the until command. The next digit in the loop is $var15
var15=$[ $var15 - 5 ]
done

**$bash -f main.sh**
```

You are seeing the operations of the until command. The next digit in the loop is 100

You are seeing the operations of the until command. The next digit in the loop is 95

You are seeing the operations of the until command. The next digit in the loop is 90

And continuing, until it reaches the final digit:

You are seeing the operations of the until command. The next digit in the loop is 5

The example has successfully tested the var15 variable in order to determine when the loop will stop - when the value of the variable drops down to zero, the until command stops right away.

```
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

**$bash -f main.sh**
100
```

You are seeing the operations of the until command. The next digit in the loop is 100