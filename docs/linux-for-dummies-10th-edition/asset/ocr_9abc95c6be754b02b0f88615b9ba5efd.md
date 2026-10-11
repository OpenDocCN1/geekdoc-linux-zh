# 4.  Run the file:

```
$ ./test6.sh
Welcome, rich
Please enjoy your visit
$
```

The case statement provides a much cleaner way of specifying the various options for each possible variable value.

# Loops

When you’re writing scripts you’ll often find yourself in a situation where it would come in handy to repeat the same commands multiple times, such as applying a command against all the files in a directory. The bash shell provides some basic looping commands to accommodate that.

# The for loop

The for statement iterates through every element in a series, such as files in a directory or lines in a text document. The format of the for command is:

```
for variable in series ; do
  commands
done
```

The variable becomes a placeholder, taking on the value of each element in the series in each iteration. The commands can use the variable just like any other variable that you define in the script. Here’s an example that shows how to use a for loop to iterate through all the files in a directory.

```
$ cat test7.sh
#!/bin/bash
# iterate through the files in the Home folder
for file in $(ls | sort) ; do
 if [ -d $file ]
 then
  echo "${file} is a directory"
 fi
 if [ -f $file ]
 then
  echo "${file} is a file"
 fi
```