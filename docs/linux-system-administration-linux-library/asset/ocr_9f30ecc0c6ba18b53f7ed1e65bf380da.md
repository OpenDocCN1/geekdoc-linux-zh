# Commands Often Used in Shell Scripts

# echo [options] string

The echo command is equally useful in scripts and on the command line. Its purpose is to display the string given as its argument. This is quite handy for showing the value of an environment variable or sending output into a piped command sequence. Let's say that you need to find out the value of the HISTSIZE variable. You can echo out its value like so:

```
echo $HISTSIZE
1000
```

The echo command was used to echo a blank separator line into a data file in the rc.local script that we discussed earlier in this chapter, as follows:

```
echo >> /etc/issue
```

echo can also be used to echo a message to the user of the script, as shown here:

```
if [ ! -e /bin/executable ];
then
echo "The file /bin/executable does not exist.
fi
```

# sort

```
sort [options] [file(s)]
```

The sort command applies the sort, as defined by the specified options, to each of the files listed and concatenates them to standard output (stdout). The options for sort include -b, which says to ignore initial blanks in the sorted lines; -c, which checks to see if the file has already been sorted; -d, which considers alpha and numeric characters; -f, ignores case by evaluating each as if it were uppercase; -n, which sorts numerically; -o, which allows you to specify an alternate output file; and -r, which reverses the sort.

Assume the following numbers must be sorted:

```
66, 567, 3, 38, 64, 543
```

A standard sort will sort the numbers incorrectly:

```
3
38
```