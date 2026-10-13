# Listing Files

We'll start by using the ls (short for list) command to list the contents of the current directory:

```
$ ls
```

The output will be similar to the following:

```
Desktop    Icon    Music    Sites
Documents  Library Pictures Temporary Items
Downloads  Movies  Public
```

We can tell that several items are in the current directory, but this output does not tell us whether these items are files or directories. To find out which of the items are files and which are directories, we can specify the -F option to ls. An option is an argument that starts with the hyphen or dash character, '-'.

The following example illustrates the use of the -F option of ls:

```
$ ls -F
```

Now the output for the directory is slightly different:

```
Desktop/    Icon    Music/    Sites/
Documents/  Library/ Pictures/ Temporary Items/
Downloads/  Movies  Public/
```

As you can see, some of the items now have a / at the end, indicating each of these items is a directory. The other items, such as Icon, have no character appended to them. This indicates that they are ordinary files.

When the -F option is specified to ls, it appends a character indicating the file type of each of the items it lists. The exact character depends on your version of ls. For ordinary files, no character is appended. For special files, a character such as @, |, or # is appended to the filename. For more information on the -F options, check the UNIX manual page for the ls command. You can do this as follows:

```
$ man ls
```

> **Options Are Case Sensitive**
> The options that can be specified to a command, such as ls, are case sensitive. When specifying an option, you need to make sure that you have specified the correct case for the option. For example, the output from the -F option to ls is different from the output produced when the -f option is specified.