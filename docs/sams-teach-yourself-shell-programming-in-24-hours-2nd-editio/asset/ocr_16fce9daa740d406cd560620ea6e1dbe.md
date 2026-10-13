```
$ ln lemonade summer_drink
$ cat summer_drink
$ ln -s lemonade in the summer
$ mv summer_drink ..
$ cat ../summer_drink
$ cat lemonade in the summer
```

As you can see from the output, the file summer_drink continues to point to the original file even after it is moved out of the directory where it was created.

When a hard link is removed, the original file that it points to is not affected; only the link is deleted. If the original file is deleted, the entry for the original file is removed, but its content remains on disk until the link is deleted. For example:

```
$ echo Pomegranates are very juicy > juicy
$ ln juicy pomegranate
$ cat pomegranate
Pomegranates are very juicy
$ rm juicy
$ cat pomegranate
Pomegranates are very juicy
cat: juicy: No such file or directory
```

As you can see the file pomegranate continues to point to the content of the file juicy even after the file juicy has been removed.

> If a file has multiple hard links to it, simply removing the file will not be sufficient to free up the disk space; you will have to remove all of the hard links to that file.

# Symbolic Links

A symbolic link or symlink is a special file that stores a pathname to another file. When a symlink is accessed, the system automatically reads the pathname stored in the symlink and accesses the file corresponding to that pathname, thus a symlink can point to any file on the system. The pathname stored in a symlink can be an absolute or relative pathname. If a relative pathname is stored, it is relative to the directory where the link is located rather than the current working directory.

The ls -l output for a symbolic link looks similar to the following:

```
lrwxrwxrwx 1 root root 9 Oct 23 13:58 /bin/ -> ./usr/bin/
```