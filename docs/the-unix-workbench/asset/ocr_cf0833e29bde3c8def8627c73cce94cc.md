# Bash Programming

```
## Start program
## You entered: 3, not what I was looking for.
## End program
```

The conditional expression `[[ $1 -eq 4 ]]` was false so code inside of the ELSE statement was run and the code in the IF statement was not run.

Between IF and ELSE statements you can also use ELIF statements. These statements act like IF statements except they’re only evaluated if preceding IF and ELIF statements have all evaluated false conditional expressions. Let’s create a brief program using ELIF:

```
#!/usr/bin/env bash
# File: simpleelif.sh

if [[ $1 -eq 4 ]]
then
  echo "$1 is my favorite number"
elif [[ $1 -gt 3 ]]
then
  echo "$1 is a great number"
else
  echo "You entered: $1, not what I was looking f\\
or."
fi
```

First let’s run the program with 4 as the first argument:

```
bash simpleelif.sh 4
```