# ## The touch Command

The touch command serves two primary purposes: It can be used to create an empty file, and it can be used to modify the last access or last modification time of an existing file. Its basic format is

```
```text
touch filename
```
```

where *filename* is the name of the file you wish to create or modify.

The touch command supports a few options that control how the last accessed or last modified times are set. See the man page for touch for full details.

# ## Creating Links

As mentioned briefly, you can create links that point to other places in the filesystem. This is useful to avoid having to type long pathnames or having to navigate through many sublevels of folders from the GUI. You can think of links as being similar to shortcuts in Windows. There are a few important differences, though, which we will look at in the following sections. The two kinds of links are hard links and soft links. Let’s look at hard links first.

# ### Hard Links

A *hard link* is a directory entry that points to the same i-node (physical location on the hard disk) as another file. There is actually only one file, but two or more directory entries point to the same physical data on the hard disk.

By default, the ln command creates hard links. Here’s an example:

```
```bash
# ln /home/foo/documents/books/fbsd/file1.txt ./file.txt
```
```

This creates an entry in the current directory called file1.txt that points to the same location on the hard disk as /home/foo/documents/books/fbsd/file1.txt. I can now access the same file by using either directory entry (presumably I would create a link like this so I only have to type vi file1.txt after I log in to edit this file rather than vi documents/books/fbsd/file1.txt). If I now use ls -l on this link, it will look something like the following:

```
```text
-rw-------   2 foo bar  26896 Mar 25 19:18  file.txt
```
```

This looks like any other plain-old file, right? That’s because it is a plain-old normal file, for all practical purposes. The only visual cue we have that this is a link is seeing the number 2 after the permissions. This indicates that two directory entries are pointing to this i-node (physical location) on the hard disk. Any changes I make to this file or its directory entry will affect the other directory entries that point to this same location. For example, if I change the permissions on this entry, the original directory entry in /home/foo/documents/books/fbsd/file1.txt will reflect the changes as well. The