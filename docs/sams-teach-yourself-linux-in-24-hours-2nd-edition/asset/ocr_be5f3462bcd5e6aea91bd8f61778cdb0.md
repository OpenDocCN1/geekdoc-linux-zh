You can also use special shell command-line quoting to label the diskette from the command line:

```
# mlabel a:'DOS DISK'
```

This is a handy way to use spaces in a diskette's label. If you want to delete files on your diskette, use the mdel command:

```
# mdel a:*.txt
```

This will delete all files ending in .txt on the diskette in the A: drive. If you need to perform more than these basic operations (such as use the floppy as a destination in an OpenLinux command line), you can also mount your diskette. For details, see the mount manual page, along with the mount command manual page.

Now that you know how to manage different filesystems, the next section covers how to manage your files.

# Managing File Ownership and Permissions

Managing files in Linux means more than moving files around the file system or keeping files grouped by similar behavior or topic. You can change which user or group owns a file or directory and whether you, your group, or others can read, write, or execute (run) your files.

The chmod (change access permissions) command, found in the /bin directory, is used to give or take away permission of groups or others to your files. Before you can begin to use the chmod program, you should understand Linux files and how Linux handles file permissions. In Hour 4, “Reading and Navigation Commands,” you learned how to get a long-format directory listing using the -l option with the ls (list) command. This option shows the mode and permissions flags of files, for example:

```
# ls -l book/*doc
-rw-r--r-- 1 bball bball 78073 Nov 16 19:58 book/24hr06or.doc
-rw-r--r-- 1 bball bball 52287 Nov 16 19:57 book/24hr11or.doc
```

The mode and permissions flags for directories and files are listed in the first 10 columns and consist of a sequence of 10 letters. (See the section “Reading File Permissions Flags” later in this chapter.) The first letter tells you the type of file.