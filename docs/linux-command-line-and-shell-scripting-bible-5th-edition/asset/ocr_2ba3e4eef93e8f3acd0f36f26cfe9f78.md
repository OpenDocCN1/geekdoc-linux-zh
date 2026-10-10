# Part III: Advanced Shell Scripting

```
The quick brown fox jumps over the lazy dog.
$ 
```

The sed editor prints the line number before the actual line of text. The %s command comes in handy if you're searching for a specific text pattern in the data stream:

```
$ cat data7.txt
This is line number 1.
This is line number 2.
This is the 3rd line.
This is the 4th line.

This is line number 1 again; we want to keep it.
This is more text we want to keep.
Last line in the file; we want to keep it.
$ 
```

```
$ sed -n '/text/{
> =
> p
> }' data7.txt
6
This is more text we want to keep.
$ 
```

By using the `-n` option, you can have the sed editor display both the line number and text for the line that contains the matching text pattern.

# Listing lines

The list (1) command allows you to print both the text and nonprintable characters in a data stream. Any nonprintable characters are shown using either their octal values, preceded by a backslash, or the standard C-style nomenclature for common nonprintable characters, such as \\t for tab characters:

```
$ cat data10.txt
This  line  contains   tabs.
This line does contain tabs.
$ 
```

```
$ sed -n '1' data10.txt
This\tline\tcontains\tabs.$
This line does contain tabs.$
$ 
```

The tab character locations are shown with the \\t. The dollar sign at the end of each line indicates the newline character. If you have a data stream that contains an escape character, the list (1) command displays it (using the octal code if necessary):

```
$ cat data11.txt
This line contains an escape character.
$ 
```

```
$ sed -n '1' data11.txt
This line contains an escape character. \a$
$ 
```