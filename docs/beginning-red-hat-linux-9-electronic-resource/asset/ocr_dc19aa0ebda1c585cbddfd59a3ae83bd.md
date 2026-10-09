This is different from the Microsoft DOS command prompt, where the cd command with no arguments merely prints the absolute path of the present directory.

We'll deal with aspects of the file system in more detail in the next chapter.

# Determining the Working Directory

Now comes the question of how to determine our current directory. For this, we use the pwd (print working directory) command, which outputs the absolute path of the present working directory. For example:

```
$ cd /home/deepak
pwd
/home/deepak
```

# Listing the Contents of a Directory

We can list the contents of a directory by using the ls (list directory contents) command. If we don't specify a directory, then ls will list the contents of the present working directory:

```
$ ls -al
total 288
drwxr-xr-x    3 deepakt users      4096 Jan 16 14:29  .
drwxr-xr-x   11 deepakt users     16384 Jan 16 14:27  ..
-rw-r-r--      1 deepakt users      49714 Jan 16 14:27 f.html
-rw-r-r--      1 deepakt users      22696 Jan 16 14:29 ff.html
drwxr-xr-x    2 deepakt users        0 Jan 16 17:10 foo
-rw-r-r--      1 deepakt users     131498 Jan 16 14:20 showthread.php.html
```

The 1s command has a multitude of options. In the example above, we've used two options:

+   - The -1 option requests that the output is the "long form" - that is, with more details than just the name of the file.
+   - The -a option lists all the files - including those beginning with a dot ( . ). Files beginning with a dot are usually configuration files. For those of us familiar with Microsoft operating systems, they are vaguely analogous to hidden files in DOS.

Don't worry if the output above doesn't make a great deal of sense - we'll be discussing file attributes in detail in Chapter 7. For now, it's enough to know that each item is either a file or a directory, and that a directory is denoted by a d in the first position of the 10-character code in the first column. In the above output, there are three directories listed - foo, the present working directory (denoted .), and the parent directory (denoted .. ). We'll discuss more options of the 1s command in the next chapter.

Also, the man command (denotes manual) describes most commands. To display the manual pages of the 1s command, we could type man 1s at the command line.