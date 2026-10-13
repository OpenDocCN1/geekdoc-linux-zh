3. There are three basic types of conditional statements: if-then-fi, if-then-else-fi, and if-then-elsif-then-fi, (as is common in the bash shell, the statement reversed is the end-of-statement delimiter, so fi ends an if statement) as exemplified here:

```
if test -x $file ; then # executable
perm="Sperm+execute"
fi
if test -o $file ; then # owned by user
info="$file is owned by $LOGNAME"
else
info="$file is not owned by $LOGNAME"
fi
if test -d $file ; then # is a directory
echo "$file is a directory"
elsif test -f $file ; then # is a file
echo "$file is a file"
else
echo "$file doesn't exist"
fi
```

The first is a straightforward conditional; if the condition (test -x $file) is true, the statement following, assigning $perm+execute to variable perm, will be executed. If it's not true, the shell will skip to the subsequent instruction.

The second is a bit more complicated, but still easy to understand: If test -o $file is true, the second line is executed. If not, the else statement causes the fourth line (for example, not owned by $LOGNAME) to be executed.

Finally, the third example (elsif) is a shorthand way of writing the following loop:

```
if test -d $file ; then
echo "$file is a directory"
else
if test -f $file ; then
echo "$file is a file"
else
echo "$file doesn't exist"
fi
fi
```

The advantage of the elsif is that it helps avoid overly deep nesting on complex statements. You can imagine if we had a script that had four or five else-if conditionals that having the last dozen lines as fi-fi-fi-fi would look odd and be potentially confusing.

4. Of course, one way to address a sequence of elsif statements is to turn the sequence into a case statement, where you can test against a number of different values in a more elegant fashion. This works in some situations, but not others.