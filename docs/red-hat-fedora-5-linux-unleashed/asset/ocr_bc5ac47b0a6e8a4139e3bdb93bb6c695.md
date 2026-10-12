# File Operators

These operators can be used as file comparison operators:

+   -d--To ascertain whether a file is a directory
+   -e--To ascertain whether a file exists
+   -f--To ascertain whether a file is a regular file
+   -o--To ascertain whether a user is the owner of a file
+   -r--To ascertain whether read permission is set for a file
+   -w--To ascertain whether write permission is set for a file
+   -x--To ascertain whether execute permission is set for a file
+   -z--To ascertain whether the file size is zero

The following examples are based on a shell program called `compare3`, which is in a directory with a file called `file1` and a subdirectory `dir1` under the current directory. Assume that `file1` has a permission of `r-x` (read and execute permission) and `dir1` has a permission of `rwx` (read, write, and execute permission).

The following is the code for the `compare3` shell program:

```
#!/bin/csh
if (-d dir1) then
    echo "dir1 is a directory"
else
    echo "dir1 is not a directory"
endif

if (-f dir1) then
    echo "file1 is a regular file"
else
    echo "file1 is not a regular file"
endif

if (-r file1) then
    echo "file1 has read permission"
else
    echo "file1 does not have read permission"
endif

if (-w file1) then
    echo "file1 has write permission"
else
    echo "file1 does not have write permission"
endif
```