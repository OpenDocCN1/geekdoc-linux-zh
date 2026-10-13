This command moves the file error_log from the directory /usr/local/httpd/logs, and the file myfile2 from the directory /priv/home/henry into the directory /tmp.

![](bbox=[0.15, 0.32, 0.22, 0.38])

# Limitations to mv

The mv command can also be used to move and rename directories with exactly the same syntax used for moving and renaming files—just give directory names instead of filenames.

Unfortunately, for this task the mv command is a little more limited than you might like it to be. It cannot move directories between physical devices; so every now and then if you try to move a directory from one location to another, UNIX's abstraction of physical devices in the file system will sneak up to bite you, and you get an error message such as:

```
Can't move directories across partitions
```

If this happens, the easiest solution is to use the copy command to copy the offending directory, and then delete the original.

# CREATING LINKS: ln

The final file management utility you will learn about in this lesson is the command used for creating links or aliases to files. The ln command is used to create links to files so that one file can appear to be in multiple locations and have multiple names.

To see the utility of this command, consider the situation in which you want your friends to look at your daily schedule. Daily or weekly, as appropriate, you can create a new file with your schedule and name it with the current date. Because you don't want to have to constantly give your friends new filenames to check your schedule, you might just create a link named myschedule, which you then point to whatever file contains