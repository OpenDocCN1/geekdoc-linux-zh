![](bbox=[0.05, 0.11, 0.8, 0.19])

The -F option causes ls to append a character to the end of certain files that indicates their type. For example, directory names have a slash ( / ) appended to them. Plain filenames appear as is. An at sign ( @ ) indicates that a file, such as xkb in the listing, is actually a link to another file.

![](bbox=[0.07, 0.34, 0.12, 0.39])

A link is a filename that refers to another file. It's like a shortcut in Windows.

An asterisk ( * ) is appended to executable files (for example, the prefdm file in the listing).

![](bbox=[0.07, 0.48, 0.12, 0.53])

The exact files you see may vary slightly depending on the kind of installation you performed during Friday night's session.

You can see even more detailed information about the files and directories with the - l option:

```
ls -l
```

For the /etc/X11 directory, a typical output from ls -l looks like the following:

![](bbox=[0.08, 0.7, 0.85, 0.83])

This listing shows considerable information about each directory entry, which can be a file or another directory. Looking at a line from the right column to the left, you see that the rightmost column shows the name of the directory entry. The date and time before the name shows its MTime, when it was last modified. The file size, in bytes, appears before the MTime.

The file's group and owner appear to the left of the file size column. The next number to the left indicates the number of links to the file or, if the entry is a directory, the number of files it contains (including . and .. ). Finally, the leftmost column shows the file's permission settings, which control who can read, write, or execute the file. The very first letter of the permission setting has one of the following special meanings:

+   - If the first letter is l, the file is a symbolic link to another file.
+   - If the first letter is d, the file is a directory.