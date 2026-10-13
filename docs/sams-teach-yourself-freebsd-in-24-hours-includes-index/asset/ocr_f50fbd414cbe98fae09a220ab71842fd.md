The first set of entries lists the type of the entry and its permissions. The first entry, Mail, starts with d, which means that the entry corresponds to a directory. The next nine spaces correspond to the permissions. There are three spaces for the owner of the file, three spaces for the group of the file, and three spaces for other, which includes everyone else. In this case, the owner has read, write, and execute permissions on this directory (rwx). The group and the user have no permissions. Who are the owner and group? Those are indicated by the third and fourth entries. In this case, the owner is murban and the group is research. (My group membership is research). In this case, this means that murban can do whatever he wants with this directory (read, write, execute), but no one else can do anything. I will explain permissions in more detail in a later hour.

The next entry after research indicates the size of the entry in bytes. After that comes the date and time that the entry was last modified. The last entry is, of course, the name of the file.

The second line deserves special mention. An entry that looks like this

```
lrwxrwxr-w 1 murban research 15 Mar 20 06:55 tyfbsd ->
/home/murban/documents/books/tyfbsd
```

indicates a symbolic link. As mentioned previously, symbolic links are like shortcuts in Windows. In this case, the entry tyfbsd is actually a shortcut to the directory /home/murban/documents/books/tyfbsd. The symbolic link allows me to get to this directory by just using tyfbsd instead of the much longer path.

# Changing Directories

To move to a different directory, use the command cd, which is short for change directory. For example, to change to the directory tyfbsd, which is a subdirectory off the current directory, you would use the command cd tyfbsd. This is called a relative path. A relative path means that the directory given to the cd command is relative to the directory you are currently in. In other words, the command is relative to the directory you are currently in, and the tyfbsd directory is a subdirectory of the current directory. The alternative is an absolute path. An absolute path always begins at the root directory. Recall that the root directory is represented by / and is the top-level directory in the system. An example of using cd with an absolute directory would be cd /tyfbsd. This would change to a directory called tyfbsd located in the root directory.

You might recall from the previous section that the double period (..) represents the parent directory of the current directory. Because of this, you can use the double period to move up one directory level to the parent of the directory you are currently in. The command to do this would be cd ... If you want to move up two directory levels, you can use cd ../.., and so on. If you want to move to a directory called my_stuff—

![](bbox=[0.88, 0.45, 0.98, 0.65])