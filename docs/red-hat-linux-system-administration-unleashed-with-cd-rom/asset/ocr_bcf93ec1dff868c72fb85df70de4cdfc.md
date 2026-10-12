# LISTING 13.2 continued

```
/dev/fd0    /mnt/floppy    ext2    noauto,owner    0 0
none        /proc          proc    defaults        0 0
none        /dev/pts       devpts  gid=5,mode=620  0 0
[tschenk@marcanthony foo]$ cat fstab | sed s'/ext2/ext3/' > fstab
[tschenk@marcanthony foo]$ ls -l
total 0
-rw-r--r-- 1 tschenk staff   0 Mar 13 23:09 fstab
```

The user is attempting to replace all occurrences of ext2 in the fstab file with ext3 without creating a temporary file. However, as you can see, instead of the expected outcome of simply replacing occurrences of the string ext2 with ext3, it ended up destroying the contents of the file. This will not occur every time, but is dependent on how the scheduler handles the running of the two commands in the pipeline. Unlike Windows, in which commands in a pipeline are executed sequentially, commands in a pipeline under Linux are executed in parallel. In the preceding case, the sed command received the first time slice, causing the output file of the sed command, fstab, to be created before the original file was read by the cat command.

# Users with Root Access

While these types of errors and the resulting data loss are bad, consider how much worse they could be if the user had root privileges like you do as the system administrator. In this case, the malformed rm command or bad pipe could have disastrous results. Consider, for example, the mistyped rm command in the previous discussion. If you were logged in as root at the time and the command was executed in /lib, this error could result in the system becoming unusable. This is also true with the malformed pipe. If the sed command were run against the /etc/passwd file and it was lost, you would have prevented all users from accessing the system. And if you do not have a backup, the situation could become even worse. It is therefore important to always double-check your commands before you hit the Enter key. In addition, you can put into place a few simple preventative measures to help avoid these errors.

# Simple Prevention Measures to Avoid User Errors

Some of these user errors can be avoided. There are a few simple techniques that could have reduced the likelihood of this type of data loss. Some of these techniques include

+   - Using aliases to require verification of destructive commands.
+   - Using RCS to track changes to important files.