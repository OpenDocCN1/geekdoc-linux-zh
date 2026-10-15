3. Enclose the shell variable in a set of double quotes. This allows the variable to be expanded but the value of the variable will be treated as single string if it contains whitespace. The whitespace must be protected so that the command line is parsed properly.

```
nawk -F: '$1 ~ /"A"$name/ {print $2}' datafile
```

Count the number of quotes. There should be an even number of single quotes and an even number of double quotes.

Here's another example:

```
oldname="Ellie Main"
newname="Eleanor Quigley"
```

+   1. Make sure the command works.

```
nawk -F: '/Ellie Main/{ $1="Eleanor Quigley"; print $0}' datafile
```

+   2. Plug in the variables.

```
nawk -F: '/$oldname/{ $1="$newname"; print $0}' datafile
```

3. Play the quoting game. Starting at the first single quote at the left, move across the line until you come to the variable $oldname and place another single quote just before the dollar sign. Put another single quote right after the last letter in the variable name.

Now move to the right and place another single quote right before the dollar sign in $newname. Put another single quote after the last character in $newname.

```
nawk -F: '/"$oldname/"{ $1="$newname"; print $0}' datafile
```

+   4. Count the number of single quotes. If the number of single quotes is an even number, each quote has a matching quote. If not, you have forgotten a step.

+   5. Enclose each of the shell variables in double quotes. The double quotes are placed snugly around the shell variable.

```
nawk -F: '/"$oldname"/ { $1=""$newname""; print $0}' datafile
```