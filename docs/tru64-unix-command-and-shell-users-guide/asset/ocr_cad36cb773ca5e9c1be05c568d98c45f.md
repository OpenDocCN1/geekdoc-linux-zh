You can edit any number of files, one at a time, without leaving the ed program. Use the e subcommand to load a file into the buffer, make your changes to the file, and use the w subcommand to save a copy of the revised file. (See Section B.2.4 for information about the w subcommand.) Then use the e subcommand again to load another file into the buffer.

# B.3.3 Using the r (read) Subcommand

Once you have started the ed program, you can use the r (read) subcommand to read a file into the buffer. The r subcommand adds the contents of the file to the contents of the buffer. The r subcommand does not delete the buffer. (Compare the r subcommand with the e subcommand, described in Section B.3.2, which deletes the buffer before it reads in another file.)

With the r subcommand, you can read a file into the buffer at a particular place. For example, the 4r cfile subcommand reads the file cfile into the buffer following line 4. The ed program then renumbers all of the lines in the buffer. If you do not use a line number, the r subcommand adds the new file to the end of the buffer's contents.

The following example shows how to use the r subcommand with a line number:

```
1,$p
The only way to stop
appending is to enter a
line that contains only
a dot.
3r cfile
44
1,$p
The only way to stop
appending is to enter a
line that contains only
The only way to stop
appending is to enter a
a dot.
-
```

The 1,$p subcommand displays the four lines of afile. Next, the 3r cfile subcommand loads the contents of cfile into the buffer, following line 3, and shows that it read 44 characters into the buffer. The next 1,$p subcommand displays the buffer's contents again, letting you verify that the r subcommand read cfile into the buffer after line 3.

If you are working the examples on your system, complete the following steps before you go to the next section:

+   1. Save the contents of the buffer in the cfile file: