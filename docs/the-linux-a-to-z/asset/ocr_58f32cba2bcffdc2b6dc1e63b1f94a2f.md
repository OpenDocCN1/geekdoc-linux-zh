# Exercises

Write shell scripts to perform each of the following actions:

+   1. Take the names of two directories as parameters. Copy all the files in the first directory into the second directory and translate all of the occurrences of the string SP in any of the files into SU during the copy.
2. Check to see if your PATH variable contains /usr/local/bin as one of the directories to search, and display a suitable message.
3. Read lines of text from the standard input device and copy them to the standard output. Precede each output line with a line number in a similar manner to cat -n (without using the cat command).
4. Accept a number in the range 2 to 15 inclusive as a parameter and draw on the standard output a square of that size using the symbols plus (+), minus (-) and vertical bar (|), so:
5. Take two command line parameters, the first of which is the name of a directory, and the second is a file size in bytes. The command should list all the regular files in the directory to which you have read access and that are smaller than the given size. You should check that only two parameters are passed to the command and that the first parameter is in fact a directory.

```
$ drawsquare 4
+--+
| |
| |
+--+
```

If the number of parameters given to the command is wrong or the parameter is not a number in the correct range, a suitable error message should be displayed and an exit status of one returned.

# Answers

1. One possible solution could be to take each source pathname in turn, take the basename from this path, and then use sed to copy the source file to the destination directory using the same base name and performing the required translation as the copy is performed:

```
for i in $1/*
do
x=`basename $i`
sed s/SP/SU/ $i >$2/$x
done
exit 0
```