```
#!/bin/bash
echo -n "Enter the first number:"
read x
echo -n "Enter the second number:"
read y
(( sum=x+y ))
echo "The result of the addition=$sum"
```

You can see from this that it is quite straigthforward to add two numbers in the bash shell.

# How to Add Multiple Values

If you want to get multiple user inputs in your script and add them, you would use loops. The next example shows how this is done:

```
#!/bin/bash
sum=0
for (( counter=1; counter<5; counter++ ))
do
    echo -n "Enter the Number:"
    read n
    (( sum+=n ))
#echo -n "$ounter "
done
printf "\n"
echo "Result is: $sum"
```

If you do not include the (( )), you wont get an addition operation. Instead it will be concatenation so make sure you double check your script before executing it.

# Bash Functions

All computer programming languages rely on functions and the Linux Shell script is no exception. Functions allow you to create blocks of code that you need to use frequently, rather than writing the same code repeatedly. In the next demonstration, you can see how these functions work in bash scripts:

```
#!/bin/bash
function Add()
{
    echo -n "Enter a Number: "
    read x
    echo -n "Enter another Number: "
    read y
    echo "Addition is: $(($x+$y))"
}

Add
```