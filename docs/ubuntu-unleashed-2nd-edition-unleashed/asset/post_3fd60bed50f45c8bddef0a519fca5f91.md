
## The while Statement

The while statement can be used to execute a series of commands while a specified condition is true. The loop terminates as soon as the specified condition evaluates to false. It is possible that the loop will not execute at all if the specified condition initially evaluates to false. You should be careful with the while command because the loop will never terminate if the specified condition never evaluates to false.

## Endless Loops Have Their Place in Shell Programs

Endless loops can sometimes be useful. For example, you can easily construct a simple command that constantly monitors the 802.11b link quality of a network interface by using a few lines of script:

```
#!/bin/sh
while :
do
  /sbin/iwconfig eth0 | grep Link | tr '\n' '\r'
done
```

The script outputs the result, and then the tr command formats the output. The result is a simple animation of a constantly updated single line of information:

```
Link Quality:92/92  Signal level:-11 dBm  Noise level:-102 dBm
```

This technique can also be used to create a graphical monitoring client for X that outputs traffic information and activity about a network interface:

```
#!/bin/sh
xterm -geometry 75x2 -e \
bash -c \
"while :; do \
/sbin/ifconfig eth0 | \
grep 'TX bytes' | \
tr '\n' '\r' ; \
done"
```

The simple example uses a bash command-line script (enabled by -c) to execute a command line repeatedly. The command line pipes the output of the ifconfig command through grep, which searches ifconfig's output and then pipes a line containing the string "TX bytes" to the tr command. The tr command then removes the carriage return at the end of the line to display the information inside an xterm X11 terminal window, automatically sized by the -geometry option:

```
RX bytes:4117594780 (3926.8 Mb)  TX bytes:452230967 (431.2 Mb)
```

Endless loops can be so useful that Linux includes a command that will repeatedly execute a given command line. For example, you can get a quick report about a system's hardware health by using the sensors command. But instead of using a shell script to loop the output endlessly, you can use the watch command to repeat the information and provide simple animation:

```
$ watch "sensors -f | cut -c 1-20"
```

The loop terminates as soon as the specified condition evaluates to True.

In pdksh and bash, the following format is used:

```
until expression
do
    statements
done
```

As you can see, the format of the until statement is similar to that of the while statement, but the logic is different: In a while loop, you execute until an expression is False, but in an until loop, you loop until the expression is True.

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
echo "result is $result"
```

The example here is identical to the example for the while statement, except that the condition being tested is just the opposite of the condition specified in the while statement.

The tcsh shell does not support the until statement.

## The repeat Statement (tcsh)

The repeat statement is used to execute only one command a fixed number of times.

If you want to print a hyphen (-) 80 times with one hyphen per line on the screen, you can use the following command:

```
repeat 80 echo '-'
```

## The select Statement (pdksh)

The select statement is used to generate a menu list if you are writing a shell program that expects input from the user online. The format of the select statement is as follows:

```
select  item in itemlist
 do
    Statements
 done
```

itemlist is optional. If it isn’t provided, the system iterates through the item entries one at a time. If itemlist is provided, however, the system iterates for each entry in itemlist and the current value of itemlist is assigned to item for each iteration, which then can be used as part of the statements being executed.

If you want to write a menu that gives the user a choice of picking a Continue or a Finish, you can write the following shell program:

```
#!/bin/ksh
select  item in Continue Finish
do
    if [ $item = 'Finish' ]; then
        break
    fi
done
```

When the select command is executed, the system displays a menu with numeric choices to the user—in this case, 1 for Continue and 2 for Finish. If the user chooses 1, the variable item contains a value of Continue; if the user chooses 2, the variable item contains a value of Finish. When the user chooses 2, the if statement is executed and the loop terminates.

## The shift Statement

The shift statement is used to process the positional parameters, one at a time, from left to right. As you’ll remember, the positional parameters are identified as $1, $2, $3, and so on. The effect of the shift command is that each positional parameter is moved one position to the left and the current $1 parameter is lost.

The shift statement is useful when you are writing shell programs in which a user can pass various options. Depending on the specified option, the parameters that follow can mean different things or might not be there at all.

The format of the shift command is as follows:

```
shift  number
```

The parameter number is the number of places to be shifted and is optional. If not specified, the default is 1; that is, the parameters are shifted one position to the left. If specified, the parameters are shifted number positions to the left.
