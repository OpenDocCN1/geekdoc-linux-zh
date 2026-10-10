number or text pattern address. The sed editor inserts the text from the file after the address.

```
```
$ cat data13.txt
This is an added line.
This is a second added line.
$
$ sed '3r data13.txt' data6.txt
This is line number 1.
This is line number 2.
This is the 3rd line.
This is an added line.
This is a second added line.
This is the 4th line.
$
```
```

The sed editor inserts into the data stream all the text lines in the data file. The same technique works when using a text pattern address:

```
```
$ sed '/number 2/r data13.txt' data6.txt
This is line number 1.
This is line number 2.
This is an added line.
This is a second added line.
This is the 3rd line.
This is the 4th line.
$
```
```

If you want to add text to the end of a data stream, just use the dollar sign address symbol:

```
```
$ sed '$r data13.txt' data6.txt
This is line number 1.
This is line number 2.
This is the 3rd line.
This is the 4th line.
This is an added line.
This is a second added line.
$
```
```

A cool application of the read (r) command is to use it in conjunction with a delete (d) command to replace a placeholder in a file with data from another file. For example, suppose that you had a form stored in a text file that looked like this:

```
```
$ cat notice.std
Would the following people:
```
```