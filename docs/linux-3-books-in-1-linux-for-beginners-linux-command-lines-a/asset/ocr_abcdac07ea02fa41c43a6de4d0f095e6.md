option since it does not check for any spelling errors.

```
[student@desktop ~]$ mkdir Drawer
[student@desktop ~]$ ls
    Drawer
```

You can see that the command creates a new directory called Drawer in the student user's home directory.

```
[student@desktop ~]$ mkdir -p Thesis/Chapter1
[student@desktop ~]$ ls -R
    Thesis    thesis_chapter1
```

When we use the option -p with the mkdir command, the parent directory Thesis, and the subdirectory Chapter1 are created simultaneously.

# Copying Files

Files can be copied on the Linux system by using the **cp** command on the command line. The command can be used to copy one or more files, and you can copy files within the same directory or from one directory to another.

You will need to specify a unique destination file. If the file already exists, the copy action will overwrite the existing file with the source file's contents.

```
[student@desktop ~]$ cd Documents
[student@desktop Documents]$ cp one.txt two.txt
```

In the above example, contents of the file one.txt are copied to the file two.txt

```
[student@desktop ~]$ cp one.txt Documents/two.txt
```

In the above example, contents of the file one.txt are copied to the file two.txt that is under the Documents directory.

# Moving Files

You can use the **mv** command to move files from one place to another. The