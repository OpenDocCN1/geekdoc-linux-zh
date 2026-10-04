```
$ ls -i backup text
backup:
    338 motd.bak
text:
    338 motd      340 newpass      340 passwd
```

If you change the contents of text/motd in the example, then the contents of the file backup/motd.bak will also be changed because it is exactly the same file.

The only problem with all this is that each filesystem (disk partition) has its own array of inodes, so that the inode numbers are only unique within a single filesystem. This means that you could not use ln to set up this kind of link between, say, text/motd under your home directory and another pathname in a different filesystem. This is because, in another filesystem, inode number 338 (the inode number of text/motd in your home directory's filesystem) would be a completely different file.

If you need to set up a link between pathnames in different filesystems it can be done, but not using the shared inode technique above. What you do in this case is to use ln -s to set up a symbolic link between the two instead. A symbolic link is one of the Linux special file types and in effect it is just a text file which contains the pathname of the other file to which it provides a link. The other file is the real file which contains all the data. All the commands that read or write the contents of a file, when they are applied to a symbolic link, will follow the link and access the real file instead. Obviously, there is some very small time penalty for having to take this extra step but it is too small to make any real difference.

When you want to create a link between two files and you want to make sure that what you do can be ported to other systems, you should use symbolic links. This is because they can be used both within a single filesystem and between separate filesystems, while inode links can only be used in the first of these situations:

```
$ ln -s text/motd backup/motd2.bak
$ ls -i backup text
backup:
    338 motd.bak    328 motd2.bak
text:
    338 motd        340 newpass      340 passwd
```

Another command that operates by manipulating inode links is mv. This command is used to move a directory link from one place to another within the same filesystem. Effectively, it performs the same function as ln to link inodes, but then removes the old link to the file:

```
$ mv text/newpass backup/passwd.bak
$ ls -i backup text
backup:
    338 motd.bak    328 motd2.bak    340 passwd.bak
```