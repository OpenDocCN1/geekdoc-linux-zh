# # Restoring Backups

Once you have performed the necessary backups of all your Linux servers, all the data are now safely stored. It is only a matter of time, however, before you will need to restore either corrupted or lost data. If you have followed the preceding instructions, the tape should automatically rewind once all the partitions have been backed up. However, if you need to rewind the tape, you should use the *mt* (for *magnetic tape*) command. You can use *mt* either to rewind or retension the tape or to forward or reverse the tape to a new location based on which partition you want to examine.

# ## Restoring tarred Files

Restoring tarred files is just as easy as tarring them up. You are not obliged to untar them immediately to see their contents; rather, tar gives you the option of printing out the tar file's contents verbosely so that you can see exactly what the single tar file contains. Using this option is a recommended practice for Linux users, if you do not entirely trust the *owner* of the file or have some doubt about where the files might be untarred upon execution of the untarring command.

To check the tar file's contents first, enter the following on the command line. This example uses the *docs.tar* file created from the *docs/* directory.

```
```
tar -tvf docs.tar
```
```

The *-t* or *--list* option prints out the files within the tar file exactly as if they were being written out to the directory. You can either use the full or abbreviated version of this option when adding the flags. *-t* and *--list* are the same command; the latter is simply the more verbose method of telling the command what sort of additional option to perform. When you use *-t*, no files will be written out to the hard disk.

If the output is agreeable and appears to be what you expected, you can extract the data and save them onto a disk. You can do so by using the *-x* or *--extract* option instead of the *-t* option. In addition, you can still place other flags, such as *-p* for retaining the original permissions. A sample restore from a tar file would look like this:

```
```
tar -xvf dp docs.tar
```
```