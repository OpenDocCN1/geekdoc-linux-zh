You can use three types of wildcards in Bash:

+   - The asterisk (*) character matches zero or more characters in a filename. That means * denotes all files in a directory.
+   - The question mark (?) matches any single character. So if you type test?, that matches any five-character text that begins with test.
+   - A set of characters in brackets matches any single character from that set. The string [aB]*, for example, matches any filename that starts with a or B.

Wildcards are handy when you want to do something to a whole lot of files. For example, to copy all the files from the /mnt/cdrom directory to the current directory, type the following:

```
cp /mnt/cdrom/* .
```

Bash replaces the wildcard character * with the names of all the files in the /mnt/cdrom directory. The period at the end of the command represents the current directory.

You can use the asterisk with other parts of a filename to select a more specific group of files. Suppose you want to use the grep command to search for the text typedef struct in all files of the /usr/include directory that meet the following criteria:

+   - The filename starts with s.
+   - The filename ends with .h.

The wildcard specification s*.h denotes all filenames that meet these criteria. Thus you can perform the search with the following command:

```
grep "typedef struct" /usr/include/s*.h
```

The string contains a space that you want the grep command to find, so you have to enclose that string in quotation marks. That way Bash does not try to interpret each word as a separate command-line argument.

The question mark (?) matches a single character. Suppose that you have four files — image1.pcx, image2.pcx, image3.pcx, and image4.pcx — in the current directory. To copy these files to the /mnt/floppy directory, use the following command:

```
cp image?.pcx /mnt/floppy
```