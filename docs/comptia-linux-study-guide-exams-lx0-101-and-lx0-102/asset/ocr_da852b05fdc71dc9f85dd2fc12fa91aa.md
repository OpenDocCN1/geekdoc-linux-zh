# Using File Management Commands

# The touch Command

Linux-native filesystems maintain three timestamps for every file:

+   - Last file-modification time
- Last inode change time
- Last access

Various programs rely on these timestamps; for instance, the make utility (which helps compile a program from source code) uses the timestamps to determine which source-code files must be recompiled if an object file already exists for a particular file. Thus, sometimes you may need to modify the timestamps. This is the job of the touch command, which has the following syntax:

```
touch [options] files
```

By default, touch sets the modification and access times to the current time. You might use this, for instance, you wanted to recompile a particular source code even though a newer object exists. If the specified files don't already exist, touch creates empty files. This can be handy if you want to create dummy files—say, to experiment with other file-manipulation commands.

You can pass various options to have it change its behavior:

Change Only the Access Time. The -a or --time=at option causes touch to change the access time, not the modification time.

Change Only the Modification Time. The -m or --time=mtime option causes touch to change the modification time, not the access time.

Do Not Create File If you don't want to create files that don't already exist, pass the -c or --no-create option.

Set the Time as The -t timestamp sets the time to the specified timestamp. This value is given in format MMDDhhmm[[CCYY]], where MM is the month, DD is the day, hh is the hour (on a 24-hour clock), mm is the minute, [[CCYY] is the year (as 2012 or 12, which are equivalent), and ss is the second. Another way to set a particular time is with the -r refile or --reference=refile option, where refile is a file whose time you want to replicate.

# File Archiving Commands

A archiving tool collects a group of files into a single "package" file that you can easily move around on a single system; back up to a readable DVD, tape, or other removable media; or transfer across a network. Linux supports several archiving commands, the most prominent being tar and cpio. The dd command, although not technically an archiving command, is similar in some ways, because it can copy an entire partition or disk into a file, or vice versa.