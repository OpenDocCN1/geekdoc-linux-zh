abcd
abcd
abcccd
abcd

Repeated a's and b's have been lost.

# dos2unix and unixdos

DOS and Windows have a different convention for newline characters from Unix and
Linux. In DOS, the newline character is a carriage return and a line feed, whereas in
Unix it is just a linefeed. What this is there can be problems when deal-
ing files from one system to the other. The programs dos2unix and unixdos
will convert (by in place) a file from one system of newlines to the other.

For example:

```
userbible:- > unixdos INDEX
```

This will silently overwrite the original file with its Unix-style line endings with the
DOS version (which you can give to your friend so he can read it in Notepad with-
outembarrassment);

If you want to keep the original file, both dos2unix and unixdos have a -n option
that enables you to specify an output file:

```
userbible:- > unixdos -n INDEX.txt
unixdos: converting file to file INDEX.txt in DOS format ...
```

You can, in fact, achieve the same result as dos2unix with tr like this:

```
cat file.txt | tr -d '\15' -outfile
```

This removes the carriage return character that has the decimal value 13 represented
ob octal \15.

# Formatting Text Files for Viewing and Printing

The commands illustrated in this section offer ways to take plain text files and tidy
them or present them differently for display or printing.