# Use Absolute Pathnames with Symbolic Links

Symbolic links are literal and are not aware of directories: A link that points to a relative path, which includes simple filenames, assumes that the relative path is relative to the directory that the link was created in (and not the directory the link was created from). In the following example the link points to the file name sum in the /tmp directory. Because there is no such file, cat gives an error message:

```
$ pwd
/home/alex
$ ln --symlink sum /tmp/s3
$ ls -l sum /tmp/s3
l rwxrwxwx 1 alex 3 Jun 12 10:13 /tmp/s3 -> sum
-rw-r-- 1 alex 38 Jun 12 09:51 sum
$ cat /tmp/s3: No such file or directory
```

The sizes and times of the last modification of the two files are different. Unlike a hard link, a symbolic link to a file does not have the same status information as the file itself.

Similarly, you can use ln to create a symbolic link to a directory. When you use the --symbolic option, ln does not care whether the file you are creating a link to is a regular file or a directory.

# Optional

# cd and Symbolic Links

When you use a symbolic link as an argument to cd to change directories, the results can be confusing, particularly if you did not realize you were using a symbolic link. Adding to the confusion is the fact that the bash, tcsh, and zsh shells handle symbolically linked directories differently when using cd.

# Symbolically Linked Directories under bash

If you use cd to change to a directory that is represented by a symbolic link, the pwd builtin lists lists the name of the symbolic link. The pwd utility /bin/pwd lists the name of the linked-to directory, not the link, regardless of how you got there:

```
$ ls -s /home/alex/grades /tmp/grades.old
$ pwd
/home/alex
$ cd /tmp/grades.old
$ pwd
/tmp/grades.old
$ /bin/pwd
/home/alex/grades
```