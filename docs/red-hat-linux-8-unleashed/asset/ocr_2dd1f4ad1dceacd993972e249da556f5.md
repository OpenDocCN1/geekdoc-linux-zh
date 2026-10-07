If you want to add the first five even numbers, you can use the following shell program in pdksh and bash:

```
#!/bin/bash
loopcount=0
result=0
until [ $loopcount -ge 5 ]
do
  loopcount=`expr $loopcount + 1`
  increment=`expr $loopcount \* 2`
  result=`expr $result + $increment`
done
```

echo "result is $result"

The example here is identical to the example for the while statement, except that the condition being tested is the opposite of the condition specified in the while statement.

The tcsh shell does not support the until statement.

# The repeat Statement (tcsh)

The repeat statement is used to execute only one command a fixed number of times.

If you want to print a hyphen (-) 80 times with one hyphen per line on the screen, you can use the following command:

```
repeat 80 echo '-'
```

# The select Statement (pdksh)

The select statement is used to generate a menu list if you are writing a shell program that expects input from the user online. The format of the select statement is as follows:

```
select item in itemlist
do
  Statements
done
```

itemlist is optional. If it is not provided, the system iterates through the item entries one at a time. If itemlist is provided, however the system iterates for each entry in itemlist and the current value of itemlist is assigned to item for each iteration, which then can be used as part of the statements executed.