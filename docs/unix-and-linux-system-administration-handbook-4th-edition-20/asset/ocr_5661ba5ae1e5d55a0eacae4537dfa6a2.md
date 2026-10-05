# Chapter 6 The Filesystem

On some systems, you can also set the setgid nonexecutable plain files to request special locking behavior when the file is opened. However, we are not aware of any common cases in which this feature is used.

# The sticky bit

The bit with octal value 1000 is called the sticky bit. It was of historical importance as a modifier for executable files on early UNIX systems. However, that meaning of the sticky bit is now obsolete and modern systems silently ignore it.

If the sticky bit is set on a directory, the filesystem won't allow you to delete or rename a file unless you are the owner of the directory, the owner of the file, or the superuser. Having write permission on directory is not enough. This helps directories like /tmp a little more private and secure.

![](bbox=[0.09, 0.343, 0.233, 0.393])

Solaris and HP-UX are slightly less stringent in their handling of sticky directories: you can delete a file in a sticky directory if you have write permission on it, even if you aren't the owner. This actually makes a lot of sense, though it makes little practical difference.

# ls: list and inspect files

The filesystem maintains about forty separate pieces of information for each file, but most of them are only useful to the filesystem itself. As a system administrator, you will be concerned mostly with the link count, owner, group, mode, size, last access time, last modification time, and type. You can inspect all of these with ls -l (or ls -d for directory; without the -d flag, ls lists the directory's contents).

An attribute time is also maintained for each file. The conventional name for this time ("ctime", short for "change time") leads people to believe that it is the file's creation time. Unfortunately, it records the time the attributes of the file (owner, mode, etc.) were last changed (as opposed to the time at which the file's contents were modified).

Consider the following example:

```
$ ls -l /bin/gzip
-rw-xr-x root 62100 May 28 2010 /bin/gzip
```

The first field specifies the file type and mode. The first character is a dash, so the file is a regular file. (See Table 6.3 on page 148 for other codes).

The next nine characters in this field are the three sets of permission bits. The order is owner-group-other, and the order of bits within each set is read-write-execute. Although these bits have only binary values, they symbolically with the letters r, w, and x for read, write, and execute. In this case, the owner has all permissions on the file and everyone else has read and execute permission.

If the setuid bit had been set, the x representing the owner's execute permission would have been replaced with an s, and if the setgid bit had been set, the x for the