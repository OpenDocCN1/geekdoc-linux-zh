This reads the *filename* file into the buffer after line *n*. If you do not specify *n*, *ed* adds the file to the end of the buffer.

# B.3.1 Using the ed (edit) Command

To load a file into the edit buffer when you start the *ed* program, enter the name of the file after the *ed* command. The *ed* command in the following example invokes the *ed* program and loads the file *afile* into the edit buffer:

```
$ ed afile
78
-
```

The *ed* program displays the number of characters that it read into the edit buffer (78).

If *ed* cannot find the file, it displays *?filename*. To create that file, use the *a* (append) subcommand (described in Section B.2.2) and the *w* (write) subcommand (described in Section B.2.4).

# B.3.2 Using the e (edit) Subcommand

Once you start the *ed* program, you can use the *e* (edit) subcommand to load a file into the buffer. The *e* subcommand replaces the contents of the buffer with the new file. (Compare the *e* subcommand with the *r* subcommand, described next in Section B.3.3, which adds the new file to the buffer.)

> Caution
> 
> When you load a new file into the buffer, the new file replaces the buffer's previous contents. Save a copy of the buffer with the *w* subcommand before you read a new file into the buffer.

In the following example, the *e cfile* subcommand reads the *cfile* file into the edit buffer, replacing *afile*. The *e afile* subcommand then loads *afile* back into the buffer, deleting *cfile*. The *ed* program returns the number of characters read into the buffer after each *e* subcommand (44 and 78):

```
e cfile
44
e afile
78
-
```

If *ed* cannot find the file, it returns *? filename*. To create that file, use the *a* (append) subcommand, described in Section B.2.2, and the *w* (write) subcommand, described in Section B.2.4.