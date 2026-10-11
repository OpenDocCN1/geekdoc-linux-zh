| Operator | Description: Expression True if... |
|---|---|
| !EXPRESSION | The EXPRESSION is false. |
| -n STRING | STRING length is greater than zero |
| -z STRING | The length of STRING is zero (empty) |
| STRING1 != STRING2 | STRING1 is not equal to STRING2 |
| STRING1 = STRING2 | STRING1 is equal to STRING2 |
| INTEGER1 -eq INTEGER2 | INTEGER1 is equal to INTEGER2 |
| INTEGER1 -ne INTEGER2 | INTEGER1 is not equal to INTEGER2 |
| INTEGER1 -gt INTEGER2 | INTEGER1 is greater than INTEGER2 |
| INTEGER1 -lt INTEGER2 | INTEGER1 is less than INTEGER2 |
| INTEGER1 -ge INTEGER2 | INTEGER1 is greater than or equal to INTEGER 2 |
| INTEGER1 -le INTEGER2 | INTEGER1 is less than or equal to INTEGER 2 |
| -d FILE | FILE exists and is a directory |
| -e FILE | FILE exists |
| -r FILE | FILE exists and has read permission |
| -s FILE | FILE exists and is not empty |
| -w FILE | FILE exists and has write permission |
| -x FILE | FILE exists and has execute permission |

With the above in mind, our previous example using if can be rewritten without square brackets as follows:

```
kali@kali:~$ cat ./if2.sh
#!/bin/bash
# if statement example 2
read -p "What is your age: " age
if test $age -lt 16
then
echo "You might need parental permission to take this course!"
fi

kali@kali:~$ chmod +x ./if2.sh

kali@kali:~$ ./if2.sh
What is your age: 15
You might need parental permission to take this course!
```

Even though this example is functionally equivalent to the example using square brackets, using square brackets makes the code slightly easier to read.

We can also perform a certain set of actions if a statement is true and another set if it is false. To do this, we can use the else statement, which has the following syntax:

```
if [ <some test> ]
then
<perform action>
else
```