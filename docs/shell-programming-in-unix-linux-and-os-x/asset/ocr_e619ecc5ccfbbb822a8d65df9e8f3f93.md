where command is an ed-style command applied to each line of the specified file. If no file is specified, standard input is assumed.

As sed applies the indicated command or commands to each line of the input, it writes the results to standard output.

Let's have a look. First, the intro file again:

```
$ cat intro
```

The Unix operating system was pioneered by Ken Thompson and Dennis Ritchie at Bell Laboratories in the late 1960s. One of the primary goals in the design of the Unix system was to create an environment that promoted efficient program development.

```
$
```

Suppose you want to change all occurrences of "Unix" in the text to "UNIX." This can be easily done in sed as follows:

```
$ sed 's/Unix/UNIX/' intro Substitute Unix with UNIX
```

The UNIX operating system was pioneered by Ken Thompson and Dennis Ritchie at Bell Laboratories in the late 1960s. One of the primary goals in the design of the UNIX system was to create an environment that promoted efficient program development.

```
$
```

Get into the habit of enclosing your sed command in single quotes. Later, you'll know when the quotes are necessary and it's better to use double quotes.

The sed command s/Unix/UNIX/ is applied to every line of intro. Whether or not the line is modified, it writes to standard output. Since it's in the data stream also note that sed makes no changes to the original file.

To make the changes, you must redirect the output from sed into a temporary file and replace the original file with the newly one created:

```
$ sed 's/Unix/UNIX/' > temp Make the changes
mv temp intro And now make them permanent
```

```
$
```

Always make sure the correct changes were made to the file before you overwrite the original, a cat of temp would have been short before the mv temp overwrite the original data file.

If your text included more than one occurrence of "Unix" on the line, the above sed would changed just the first occurrence to "UNIX." By appending the global option g to the end of the substitute command s, you can ensure that multiple occurrences on a line will be changed.