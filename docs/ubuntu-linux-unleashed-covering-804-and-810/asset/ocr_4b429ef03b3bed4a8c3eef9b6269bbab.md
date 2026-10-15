That shows four matches and prints a lot of information about each of them. The first row shows the directory; you can tell it is a directory because its file attributes starts with a d. The `rwxrwxr-x` following that shows the access permissions, and this has special meanings because it is a directory. Read access for a directory allows users to see the directory contents, write access allows you to create files and subdirectories, and execute access allows you to cd into the directory. If a user has execute access but not read access, he will be able to cd into the directory but not list files.

Moving on, the next number on the line is 24, which also has a special meaning for directories: It is the number of subdirectories, including . and ... After that is paul paul, which is the name of the user owner and the group owner for the directory. Next is the size and modification time, and finally the directory name itself.

The next line shows the file copying, and most of the numbers have the same meaning, with the exception of the 1 immediately after the access permissions. For directories, this is the number of subdirectories, but for files this is the number of hard links to this file. A 1 in this column means this is the only filename pointing to this inode, so if you delete it, it is gone.

Ubuntu comes configured with a shortcut command for `ls -l`: `ll`.

The `--sort` parameter allows you to reorder the output from the default alphabetical sorting. You can sort by various things, although the most popular are extension (alphabetically), size (largest first), and time (newest first). To flip the sorting (making size sort by smallest first), use the `-r` parameter also. So, this command lists all `.ogg` files, sorted smallest to largest:

```
ls --sort size -r *.ogg
```

Finally, the `-R` parameter recurses through subdirectories. For example, typing `ls /etc` lists all the files and subdirectories in `/etc`, but `ls -R /etc` lists all the files in and subdirectories in `/etc`, all the files and subdirectories in `/etc/acpi`, all the files and subdirectories in `/etc/acpi/actions`, and so on until every subdirectory has been listed.

# Reading Manual Pages with man

Time for a much-needed mental break: The man command is easy to use. Most people use only the topic argument, like this: `man gcc`. However, two other commands work closely with man that are very useful—whatis and apropos.

The whatis command returns a one-line description of another command, which is the same text you get at the top of that command’s man page. For example:

```
[paul@caitlin ~]$ whatis ls
ls      (1) - list directory contents
```

The output then explains what ls does but also provides the man page section number for the command so you can query it further.