```
$ date | tr -s ` `
Sun Jun 4 17:27:23 BST 1995
```

The cut command can now be used with a space field delimiter to extract the time of day field (field four):

```
$ date | tr -s ` ` | cut -d` ` -f4
17:27:23
```

The output from this pipeline is now a string which itself consists of three colon delimited fields of which we want to extract the value in the middle field. Again, cut is the ideal solution, as follows:

```
$ date | tr -s ` ` | cut -d` ` -f4 | cut -d: -f2
27
```

A simpler solution to the same problem will still use cut but relies on noticing that all the fields in the output from date are of fixed size. Even when numeric fields are less than 10, so that they are only one digit instead of two, the sizes of the fields are maintained by padding them out. This allows for a solution which uses the -b switch to cut with a range of byte positions carefully calculated to coincide with the field of interest (bytes 15 to 16 in this example):

```
$ date | cut -b15-16
27
```

# 5.3.2 Comparing File Contents

There are several commands available for comparing the contents of two files for any differences. The simplest command is effectively used just to tell you whether or not two files are the same. This command is called cmp. All it does is to compare the two files given as parameters byte by byte until it either finds a difference or until it reaches the end of the files. The general form of the command is:

```
cmp file1 file2
```

If either file1 or file2 is just a hyphen (-) then the text for this file will be taken from the standard input device, which will be from the keyboard unless input redirection is used. The output from the cmp command is the first byte and the line number where the two files differ.

If the lines in the two files to be compared are sorted into order then it is possible to use the comm command to do the comparison between them. The general form for the comm command is:

```
comm options file1 file2
```