-a or -A option, you will not see the hidden files (that is, those with names starting with a dot). It can be easy to forget about this possibility — for example, consider the following:

```
user@bible:-> rmdir directory/
rmdir: directory/: Directory empty
user@bible:-> cd directory/
user@bible:-> ls
user@bible:>
user@bible:-> ls -a
.. .file
```

Here we tried to remove the directory that appeared to be empty because the ls command on its own produced no output. But -a shows that there is a hidden file in it, which is why the rmdir command failed (rmdir removes only empty directories).

As mentioned in Chapter 2, symbolic links are objects that point to other files and directories. In a standard directory list, symbolic links show as regular files, but ls provides the -l option to provide more information about files and directories as well as help you identify symbolic links in the directory. For example, create a symbolic link in the directory and then look at it with the standard ls command:

```
user@bible:~/directory ln -s ../other/file link
user@bible:~/directory touch file
user@bible:~/directory ls
file
```

Using the -l command clearly shows that this file is a symbolic link:

```
total 0
-rw-r--r-- 1 user 2024-06-20 10:10 file
lrwxrwxr-x 1 user 2024-06-20 10:32 link -> ../otherdir/file
```

Unless you are looking at a directory with a very large number of files in it, ls -la is a good way to use the ls command. If there is any unexpected about the sizes or ownership of the files, you will be able to notice it, and dot files will be displayed.

The -t option to ls can be very useful. Suppose, for example, you have recently done something that has caused a file to be created in a large directory, but you have forgotten or dont know the name of the file. The ls -lt command lists the files in order of modification date and time, so the new or newly modified files will be at the top of the listing.