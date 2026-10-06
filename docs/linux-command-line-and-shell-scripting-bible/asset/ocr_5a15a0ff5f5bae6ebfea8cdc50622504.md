Here's an example that prints only the first two lines of a data stream to a text file:

```
$ sed '1,2w test' data6
This is line number 1.
This is line number 2.
This is line number 3.
This is line number 4.
$ cat test
This is line number 1.
This is line number 2.
$
```

Of course, if you don't want the lines to display on STDOUT, you can use the -n option for the sed command.

This is a great tool to use if you need to create a data file from a master file on the basis of common values, such as those in a mailing list:

```
$ cat data10
Blum, Katie Chicago, IL
Mullen, Riley West Lafayette, IN
Snell, Haley Ft. Wayne, IN
Woenker, Matthew Springfield, IL
Wisecarper, Emma Grant Park, IL
$ sed -n '//w INustomers' data10
$ cat INustomers
Mullen, Riley West Lafayette, IN
Snell, Haley Ft. Wayne, IN
$
```

The sed editor writes to a destination file only the data lines that contain the pattern.

# Reading data from a file

You've already seen how to insert data into and append text to a data stream command line. The command (r) allows you to insert data contained in a separate file.

The format of the read command is:

```
[address]r filename
```

The filename parameter specifies either an absolute or relative pathname for the file that contains the data. You can't use a range of addresses for the read command. You can only specify a single line number or text address. The sed editor inserts the text from the file after the address.

```
$ cat datall
This is an added line.
This is the second added line.
$ sed '3r datall' data6
```