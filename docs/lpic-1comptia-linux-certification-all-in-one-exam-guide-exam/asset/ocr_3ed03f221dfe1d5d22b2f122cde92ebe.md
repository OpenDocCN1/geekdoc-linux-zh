Of course, bash does let you declare and type the variable if you want to. This is done using the declare command in the script. This can be useful if you want to have the user enter numbers in a read command. The issue here is that the bash shell interprets anything entered at the read command as text, even if the user enters a number. Consider this script:

```
#!/bin/bash
#A script that adds variables together.
echo "Enter a number:"
read NUM1
echo "Enter a second number:"
read NUM2
TOT=$NUM1+$NUM2
echo "The sum of these numbers is " $TOT
exit 0
```

When run, this script asks the user for two numbers, adds them together and assigns the result to a variable named TOT, and echoes the value of TOT on the screen. Notice what happens when the script is run in Figure 14-3.

Because we didn't declare the NUM1, NUM2, or TOT variables, bash treated them all as simple text. No arithmetic took place; the text values of each variable were concatenated together into a single text string. However, if we declare these variables and type them as integers, something very different will happen. Consider a revised version of this script, shown here:

```
#!/bin/bash
#A script that adds variables together.
declare -i NUM1
declare -i NUM2
declare -i TOT
echo "Enter a number:"
read NUM1
echo "Enter a second number:"
read NUM2
TOT=$NUM1+$NUM2
echo "The sum of these numbers is " $TOT
exit 0
```

Notice that NUM1, NUM2, and TOT are declared at the beginning of the script using the -i (integer) option. Now the bash shell will interpret the user's input as a whole number, not as text. When we use the + operator on the variables in the script, they are actually added, not just concatenated, as shown in Figure 14-4.

# Figure 14-3

The results of not
declaring variables

![](bbox=[0.37, 0.78, 0.94, 0.88])