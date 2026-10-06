# Part III Advanced Shell Scripting

By using the -n option you can have the sed editor display only the line number and text for the line that contains the matching pattern.

# Listing lines

The list command (l) allows you to print both the text and nonprintable ASCII characters in a data stream. Any nonprintable characters are shown using either their octal values, preceded by a backslash, or the standard C-style nomenclature for common nonprintable characters, such as \t for tab characters:

```
$ cat data8
This line contains tabs.
$ sed -n '1' data8
This$line\tcontains\tabs.
$
```

The tab characters are shown with the \t nomenclature. The dollar sign at the end of the line indicates the newline character. If you have a data stream that contains an escape character, the list command displays it using the octal code:

```
$ cat data9
This line contains an escape character
$ sed -n '1' data9
This line contains an escape character \033[44m$
$
```

The data9 file contains an escape control code (see Chapter 15) to change the display color. When you use the cat command to display the text file, you don't see the escape control code; it just changes the color of the display.

However, using the list command you can display the escape control code used. The \033 is the octal value of the ASCII code for the escape key.

# Using files with sed

The substitution command contains flags that allow you to work with files. There are also regular sed commands that let you do without having to substitute text.

# Writing to a file

The w command is used to write lines to a file. The format for the w command is:

```
[address]w filename
```

The filename can be specified as either a relative or absolute pathname, but in either case the person running the sed editor must have write permissions for the file. The address can be any type of addressing used in sed, such as a single line number, a text pattern, or a range of line numbers or text patterns.