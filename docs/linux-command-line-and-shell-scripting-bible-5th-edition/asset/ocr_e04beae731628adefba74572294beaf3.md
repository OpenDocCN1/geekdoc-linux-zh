## Printing lines
Similar to the p flag in the substitution command, the p command prints a line in the sed editor output. The most common use for the print command is for printing lines that contain matching text from a text pattern:

```
```
$ sed -n '/number 3/p' data
This is line number 3.
$
```

```

The print command allows you to filter only specific lines of data from the input stream.

## Writing to a file
The w command is used to write lines to a file. Here’s the format for the w command:

```
```
[address]w filename
```

```

The filename can be specified as either a relative or absolute pathname, but in either case, the person running the sed editor must have write permissions for the file. address can be any type of addressing method used in sed, such as a single line number, a text pattern, or a range of line numbers or text patterns.

Here’s an example that prints only the first two lines of a data stream to a text file:

```
```
$ sed '1,2w test' data
```

```

The output file test contains only the first two lines from the input stream.

## Reading from a file
You’ve already seen how to insert and append text into a data stream from the sed command line. The read command (r) allows you to insert data contained in a separate file.

Here’s the format of the read command:

```
```
[address]r filename
```

```

The filename parameter specifies either an absolute or relative pathname for the file that contains the data. You can’t use a range of addresses for the read command. You can specify only a single line number or text pattern address. The sed editor inserts the text from the file after the address.

```
```
$ sed '3r data' data
```

```

The sed editor inserts the complete text from the data file into the data1 file, starting at line 3 of the data1 file.