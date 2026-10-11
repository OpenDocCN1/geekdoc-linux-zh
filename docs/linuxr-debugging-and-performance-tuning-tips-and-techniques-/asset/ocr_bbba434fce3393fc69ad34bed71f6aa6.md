5.1 Considering Directory Contents

125

# 5.1.3.2 Dot and Dot-Dot

Rounding off the discussion of links, let’s look at how the ‘. ’ and ‘..’ special names are managed. They are really just hard links. In the first case, ‘. ’ is a hard link to the directory containing it, and ‘..’ is a hard link to the parent directory. The operating system creates these links for you; as mentioned earlier, user-level code cannot create a hard link to a directory. This example illustrates the links:

```
$ pwd
/tmp
$ ls -ldi /tmp
225345 drwxrwxrwt 14 root root 4096 May 4 16:15 /tmp
$ mkdir x
$ ls -ldi x
52794 drwxr-xr-x 2 arnold devel 4096 May 4 16:27 x
$ ls -ldi x/ ..
52794 drwxr-xr-x 2 arnold devel 4096 May 4 16:27 x/
225345 drwxrwxrwt 15 root root 4096 May 4 16:27 ../
```

The root’s parent directory (.. ) is a special case; we defer discussion of it until Chapter 8, “Filesystems and Directory Walks,” page 227.

# 5.1.4 File Renaming

Given the way in which directory entries map names to inode numbers, renaming a file is conceptually quite easy:

+   1. If the new name for the file names an existing file, remove the existing file first.
+   2. Create a new link to the file by the new name.
+   3. Remove the old name (link) for the file. (Removing names is discussed in the next section.)

Early versions of the mv command did work this way. However, when done this way, file renaming is not atomic; that is, it doesn’t happen in one uninterruptible operation. And, on a heavily loaded system, a malicious user could take advantage of race conditions,¹ subverting the rename operation and substituting a different file for the original one.

> ¹A race condition is a situation in which details of timing can produce unintended side effects or bugs. In this case, the directory, for a short period of time, is in an inconsistent state, and it is this inconsistency that introduces the vulnerability.