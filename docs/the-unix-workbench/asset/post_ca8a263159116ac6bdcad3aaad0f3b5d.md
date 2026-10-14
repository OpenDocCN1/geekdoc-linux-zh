
#!/usr/bin/env bash
# File: condexif.sh

if [[ $1 -gt 3 ]] && [[ $1 -lt 7 ]]
then
    echo "$1 is between 3 and 7"
elif [[ $1 =~ "Jeff" ]] || [[ $1 =~ "Roger" ]] || [[ $1 =~ "Brian" ]]
then
    echo "$1 works in the Data Science Lab"
else
    echo "You entered: $1, not what I was looking for."
fi

Now let’s test this script with a few different arguments:

```
bash condexif.sh 2
bash condexif.sh 4
bash condexif.sh 6
bash condexif.sh Jeff
bash condexif.sh Brian
bash condexif.sh Sean
```

```
## You entered: 2, not what I was looking for.
## 4 is between 3 and 7
## 6 is between 3 and 7
## Jeff works in the Data Science Lab
## Brian works in the Data Science Lab
## You entered: Sean, not what I was looking for.
```

The conditional execution operators work just like they would on the command line. If the entire conditional expression evaluates to the equivalent of true then the code within the IF statement is executed, otherwise it is skipped.

Finally we should note that IF/ELIF/ELSE statements can be nested inside of other IF statements. Here’s a small example of a program with nested statements:

```
#!/usr/bin/env bash
# File: nested.sh

if [[ $1 -gt 3 ]] && [[ $1 -lt 7 ]]
then
    if [[ $1 -eq 4 ]]
    then
        echo "four"
    elif [[ $1 -eq 5 ]]
    then
        echo "five"
    else
        echo "six"
    fi
else
    echo "You entered: $1, not what I was looking for."
fi
```

Now let’s run it a few times:

```
bash nested.sh 2
bash nested.sh 4
bash nested.sh 6
```

```
## You entered: 2, not what I was looking for.
## four
## six
```

In order to get to the inner IF statement, the conditions for the outer IF statement must be met first (the first argument for the script must be between 3 and 7). As you can see combining variables, arguments, conditional expressions, and IF statements allow you to write more powerful Bash programs.

# Summary

+   - All Bash programs have an exit status. true has an exit status of 0 and false has an exit status of 1.
+   - Conditional execution uses two operators: AND (&&) and OR (||) which you can use to control what command get executed based on their exit status.
+   - Conditional expressions are always in double brackets ([[ ]]). They have exit an exit status of 0 if they contain a true assertion or 1 if they contain a false assertion.
+   - IF statements evaluate conditional expressions. If an expression is true then the code within an IF statement is executed, otherwise it is skipped.
+   - ELIF and ELSE statements also help control the flow of a Bash program, and IF statements can be nested within other IF statements.

```
echo ${plagues[0]}
```

# ## blood

Notice that the first element has an index of 0. You can get any of the elements this way, for example the fourth element:

```
echo ${plagues[3]}
```

# ## flies

To get all of the elements of plagues use a star (*) between the square brackets:

```
echo ${plagues[*]}
```

```
## blood frogs lice flies sickness boils hail locusts darkness death
```

You can also change an individual elements in the array by specifying their index with square brackets:

```
echo ${plagues[*]}
plagues[4]=disease
echo ${plagues[*]}
```

```
dwarfs=(grumpy sleepy sneezy doc)
echo ${dwarfs[*]}
dwarfs+=(bashful dopey happy)
echo ${dwarfs[*]}
```

```
## grumpy sleepy sneezy doc
## grumpy sleepy sneezy doc bashful dopey happy
```

# Summary

+   - Arrays are a linear data structure with ordered elements which can be stored in variables.
+   - The each element of an array has an index and the first index is 0.
+   - Individual elements of an array can be accessed using their index.

# Exercises

+   1. Write a bash script where you define an array inside of the script, and the first argument for the script indicates the index of the array element that is printed to the console when the script is run.
+   2. Write a bash script where you define two arrays inside of the script, and the sum of the lengths of the arrays are printed to the console when the script is run.
