# CHAPTER 5 | Managing files from the Command Line

[user@host Documents]$

> WARNING
If you specify both the -i and -f options, the -f option takes priority and you will not be prompted for confirmation before rm deletes files.

In the following example, the rmdir command only removes the directory that is empty. Just like the earlier example, you must use the rm -r command to remove a directory that contains content.

```
[user@host Documents]$ pwm
/home/student/Documents
[user@host Documents]$ rmdir ProjectX
[user@host Documents]$ rmdir ProjectX
rmdir: failed to remove ProjectX': Directory not empty
[user@host Documents]$ rm -r ProjectX
[user@host Documents]$ ls -LR
:
total 0
[user@host Documents]$
```

> NOTE
The rmdir command with no options cannot remove an empty directory. You must use the rmdir command, rm -d (which is equivalent to rmdir), or rm -r.

# REFERENCES
cp(1), mkdir(1), mv(1), rm(1), and rmdir(1) man pages