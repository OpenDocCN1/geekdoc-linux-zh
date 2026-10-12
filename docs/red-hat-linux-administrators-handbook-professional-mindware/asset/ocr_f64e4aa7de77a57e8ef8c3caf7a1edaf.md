# stat

**Syntax:** stat file

This program displays various statistics on a file or directory. For example,

```
stat foo.txt
```

displays the following output:

```
File: "foo.txt"
  Size: 4447232      Filetype: Regular File
  Mode: (0644/-rw-r----)  Uid: (  0/root)   Gid: (  0/root)

Device: 3,0   Inode: 16332     Links: 1

Access: Mon Mar  1 21:39:43 2000 (00000.02:32:30)
Modify: Mon Mar  1 22:14:26 2000 (00000.01:57:47)
Change: Mon Mar  1 22:14:26 2000 (00000.01:57:47)
```

As you can see, this output displays the file access, modification, change date, size, owner and group information, permission mode, and so on.

# strings

**Syntax:** strings filename

The strings command prints character sequences that are at least four characters long. This utility is used mainly to describe the contents of non-text files.

# tail

**Syntax:** tail [-count | -nr] filename

The tail command displays the end of a file. By default, tail displays the last 10 lines of a file. To display the last 50 lines of the file doc.txt, issue this command:

```
tail -50 doc.txt
```