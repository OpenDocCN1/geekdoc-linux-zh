# Advanced Bash-Scripting Guide

```
# Same restrictions apply for deleting the file.

chmod 1777 directory-name
# Gives everyone read, write, and execute permission in directory,
# however also sets the "sticky bit"
# This means that only only the owner of the directory,
# owner of the file, and, course, root
# can delete any particular file in that directory.

chmod 111 directory-name
# Gives everyone execute-only permission in a directory.
# This means that you can execute and READ the files in that directory
# ++(execute necessarily includes read permission)
# ++ because you cannot execute a file without being able to read it)
# But you can't list the files or search for them with the "find" command.
# These restrictions do not apply to root.

chmod 000 directory-name
# No permissions at all for that directory.
# Can't read, write, or execute files in it,
# Can't even list files in or "cd" to it.
# But, you can rename (mv) the directory
# ++ or delete it if it is empty.
# ++ you can symlink to files in the directory,
# ++ you can't read, write, or execute the symlinks.
# These restrictions do not apply to root.
```

Change file attributes is analogous to chmod but with different options and a different invocation syntax, and it works only on ext2filesystems.

One particularly interesting chattr is i. chattr +filename marks the file as immutable. The file cannot be modified, linked to, or deleted, not even by root. This file attribute can be set or removed only by root. In a similar fashion, the option marks the file as append only.

```
chattr +i file.txt

rm file.txt

rm: remove write-protected regular file `file.txt`? y
rm: cannot remove `file.txt`: Operation not permitted
```

If a file has the s (secure) attribute set, then when it is deleted its block is overwritten with binary zeros. [72]

If a file has the u (undelete) attribute set, then when it is deleted, its contents can still be retrieved (undeleted).

If a file has the c (compress) attribute set, then it will automatically be compressed on writes to disk, and uncompressed on reads.

+   - The file attributes with chattr do not show in a file listing (ls -l).

Creates links to pre-existing files. A "link" is a reference to a file, an alternate name for it. The In command permits referencing the linked file by more than one name and is a superior alternative to aliasing (see Example 4-6).

# Chapter 16. External Filters, Programs and Commands