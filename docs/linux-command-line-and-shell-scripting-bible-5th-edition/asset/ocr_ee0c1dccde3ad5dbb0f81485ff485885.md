```
fi
$ ./DoubleBrackets.sh
You are using the Bash Shell version 5 series.
$
```

Notice in the preceding script that double equals signs (==) are used. These double equals signs designate the string to the right (5.*) as a pattern, and pattern matching rules are applied. The double bracket command matches the $BASH_VERSION environment variable to see whether it starts with a 5. string. If so, the comparison succeeds, and the shell executes the then section commands.

# Considering the case Command

Often, you'll find yourself trying to evaluate a variable's value, looking for a specific value within a set of possible values. In this scenario, you end up having to write a lengthy if-then-else statement, like this:

```
$ cat LongIf.sh
#!/bin/bash
# Using a tedious and long if statement
#
if [ $USER == "rich" ]
then
    echo "Welcome $USER"
    echo "Please enjoy your visit."
elif [ $USER == "barbara" ]
then
    echo "Hi there, $USER"
    echo "We're glad you could join us."
elif [ $USER == "christine" ]
then
    echo "Welcome $USER"
    echo "Please enjoy your visit."
elif [ $USER == "tim" ]
then
    echo "Hi there, $USER"
    echo "We're glad you could join us."
elif [ $USER == "testing" ]
then
    echo "Please log out when done with test."
else
    echo "Sorry, you are not allowed here."
fi
$ ./LongIf.sh
Welcome christine
Please enjoy your visit.
$
```