When you create a file, you create a hard link in a directory to a data file elsewhere on disk. That’s the purpose of the duplication in Solaris’s file system directory tree. It doesn’t matter how you create the file; whether you use the copy command, the vi editor, or the New File command in the File Manager, you still create a link. Because the copy command also creates links, you might wonder what the difference between the link command and the copy command is. The link command does not create a copy of a file as the copy command does. Any command that includes a filename starts a program that passes the filename as a pointer to the location on disk where the data for that file is found. Symbolic links, therefore, offer a convenient method for allowing multiple points of access to data; in other words, they allow users to share files.

> NOTE If you create a link to allow other people to share a file, don’t forget that you have to provide appropriate access permissions to the parent directory of that file.

The ln (link) command creates a hard link to an existing file. The syntax for the link command is as follows:

```
In <options> <pathname>/<filename pathname>/<linkname>
```

Use of the link command without the -s option creates another pointer (a hard link) to a preexisting file, not a copy of that file.

When you use the -s option, you create a symbolic link. In the following example, a symbolic link is created and the list command is used to display information about the link file. You can substitute a directory name (<directoryname>) for the filename (<filename>) and create a symbolic link to that directory. Notice that there is an l before the permission list for a link file, a pointer appears after the filename, and the original filename is displayed, as shown:

```
# ln -s /test/myfile
# ls -l myfile /test/myfile
-rw-r--	1	root	other	1054	Dec 22 01:12 /test/myfile
lrwxrwxrw	1	root	other	12	Dec 22 01:14 myfile -> /test/myfile
```

All of the links to the same file show the same file information—including access permissions, owner, group—and are stamped with the date and time the link was created. Two or more links to the same file look the same in all respects but the following: The inode number for each is different, the date and time stamp are different, and the links are owned by different owners/groups than the person who created them. If you delete a link from a set of links, you can still access the original file from any of the