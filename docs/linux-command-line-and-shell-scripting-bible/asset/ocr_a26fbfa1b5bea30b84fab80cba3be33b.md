# Viewing file statistics

You've already seen that the ls command can be used to provide lots of useful information about files, there's still more information that you can't see in the ls command (or at least not at all).

```
$ stat test10
File: "test10"
Blocks: 8  Regular File
Size: 6
Device: 306h/774d  Inode: 1954891  Links: 2
Access: (0644/-rw-r--)Uid: (501/ rich) Gid: (501/ rich)
Access: Sep 1 12:10:25 2007
Modify: Stat Sep 1 12:11:17 2007
Change: Stat Sep 1 12:16:42 2007
```

The stat command provides a complete rundown of the status of a file on the filesystem:

The results from the stat command just shows everything you'd want to know about the file being examined, even down the major and minor device numbers of the device where the file is being stored.

# Viewing the file type

Despite all the information the stat command produces, there's still one piece of information missing - the file type. Before you go charging off trying to list out a 1000-byte file, it's usually good idea to get a handle on what type of file it is. If you try to list a binary file, and possibly even lock up your terminal emulator.

The file command is a handy little utility to have around. It has the ability to peek inside of a file and determine just what kind of file it is:

```
$ file test1
test1: ASCII text
$ file myscript
myscript: Bourne shell script executable
$ file myprog
myprog: ELF 32-bit LSB executable, Intel 80386, version 1 (SYS), dynamically linked (using shared libs), not stripped
```

The file command classifies files into three categories:

+   - Text files: Files that contain printable characters
- Executable files: Files that you can run on the system
- Data files: Files that contain nonprintable binary characters, but that you can't run on the system