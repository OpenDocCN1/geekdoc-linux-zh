other links. However, if you delete the original file, all of the links stop working but the link files do not also get deleted.

You can also create a link in the CDE by using the Copy as Link command on the Select menu for files and folders. Links created with this command are symbolic links (see Chapter 7 for a description of the Copy as Link command). When you right-click a link in the File Manager window, the pop-up menu includes a Properties command, but the Properties command is not included on the pop-up menu of a link placed on the workspace.

Symbolic links work around one of the limitations of hard links: A hard link can't be a pointer to a directory. Symbolic links also allow you to link to a file that is located anywhere in the file system, or even on other file systems. You can even point a symbolic link to a nonexistent file, which is helpful when a file is removed from the file system and then restored. When you restore the file, you don't have to re-create the link. Hard links can only be applied to files on the same file system. Because Solaris uses multiple file systems, each with its own inode tables and its own file system hierarchy, hard links severely limit your flexibility.

The rm (remove file) command may be used to delete a hard link. If you remove the last hard link to the original file, Solaris deletes the data file as well. The data is no longer available on your system as a file, and Solaris releases the space on disk that the file occupies. If you delete that last hard link, even if there are any symbolic links to the original file, Solaris still deletes the data file. In the CDE, Solaris will show a broken link icon for that symbolic link, as shown in the following graphic. If you're working in the CDE and you try to delete the last hard link to a file, Solaris will warn you that it will delete the original file and ask you for a confirmation before it does so.

![](bbox=[0.46, 0.65, 0.64, 0.75])

# ## Disk Storage

In the sections that follow, I'll describe how Solaris stores data on disk in file systems. After describing the various types of file systems available, I'll show you how these file systems are written to disk and the various ways you can manage files in file systems.