Wildcards are handy when you want to perform a task on a group of files. To copy all the files from a directory named /mnt/cdrom to the current directory, for example, type the following:

```
cp /mnt/cdrom/* .
```

Bash replaces the wildcard character * with the names of all the files in the /mnt/cdrom directory. The period at the end of the command represents the current directory.

You can use the asterisk with other parts of a filename to select a more specific group of files. Suppose you want to use the grep command to search for the string typedef struct in all files of the /usr/include directory that meet the following criteria:

+   - The filename starts with s.
+   - The filename ends with .h.

The wildcard specification s*.h denotes all filenames that meet these criteria. Thus, you can perform the search with the following command:

```
grep "typedef struct" /usr/include/s*.h
```

The string contains a space you want the grep command to find, so you have to enclose that string in quotation marks. This method ensures that Bash does not try to interpret each word in the string as a separate command-line argument.

Although the asterisk (*) matches any number of characters, the question mark (?) matches a single character. Suppose you have four files — image1.pcx, image2.pcx, image3.pcx, and image4.pcx — in the current directory. To copy these files to the /mnt/floppy directory, use the following command:

```
cp image?.pcx /mnt/floppy
```

Bash replaces the single question mark with any single character and copies the four files to /mnt.

The third wildcard format — [...] — matches a single character from a specific set. You may want to combine this format with other wildcards to narrow down the matching filenames to a smaller set. To see a list of all filenames in the /etc/X11/xdm directory that start with x or X, type the following command:

```
ls /etc/X11/xdm/[xX]*
```