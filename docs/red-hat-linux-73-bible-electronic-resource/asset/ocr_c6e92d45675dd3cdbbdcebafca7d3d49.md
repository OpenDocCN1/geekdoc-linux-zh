| Operator | What Is Being Tested? |
| --- |
| var1 -le var2 | Is the first variable less than or equal to the second variable? |
| var1 -lt var2 | Is the first variable less than the second variable? |
| var1 -ne var2 | Is the first variable not equal to the second variable? |
| | |

Here are some examples that demonstrate the uses of the if statement and a test expression:

```
if [ -x /sbin/ifconfig ]
if [ $4 -eq "n1" ]
if [ $# -gt 2 ]
if [ -z $HOSTNAME ]
```

In the previous example, the first statement checks if the /sbin/ifconfig program is executable. The second example checks if the string value n1 is equal to the value stored in $4 (the fourth command-line argument). The next line checks if the number of command-line arguments (represented by the $# variable) is greater than two. The last example determines if the variable $HOSTNAME is empty.

# The case command for nested if statements

Another frequently used construct is the case command. Similar to a switch statement in programming languages, this can take the place of several nested if statements. A general form of the case statement is as follows:

```
case "VAR" in
    Result1)     { body }
        ;
    Result2)     { body }
        ;
    *)           { body }
        ;
esac
```

An example of the case command follows. This fragment of code sets the TYPE and RCFILE variables based on the user's default shell as reported in the seventh (colon-separated) field of the /etc/passwd file:

```
Shell=`grep "^$USER:" /etc/passwd | awk -F: '{ print $7 }'`
    case "$Shell" in
        /bin/sh)     TYPE=Bourne
            RCFILE=".profile"
            ;;
        /bin/csh)    TYPE=C
            RCFILE=".cshrc"
```