The -r option displays the output in reverse order. By default, -r displays all the lines in the file, not just 10 lines. For instance, to display the entire contents of the file doc.txt in reverse order, use the following:

```
tail -r doc.txt
```

To display the last 10 lines of the file doc.txt in reverse order, use:

```
tail -10r doc.txt
```

The -f option is useful when you are monitoring a file. With this option, tail will wait for new data to be written to the file. As new data is added to the file, tail displays the data to the screen. To stop tail from monitoring a file, press Ctrl+C (the intr key), because the tail command will not stop on its own.

# touch

Syntax:

```
touch file or directory
```

The touch command updates the timestamp of a file or directory. If the named file does not exist, it will be created as an empty file.

# umask

See the section on setting default file permissions for users in Chapter 3.

# uniq

Syntax:

```
uniq (-c) filename
```

The uniq command compares adjacent lines and displays only one unique line. When used with the -c option, uniq counts the number of occurrences. A file that has the contents