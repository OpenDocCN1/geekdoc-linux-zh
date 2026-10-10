# Part III Administration

+   List only available and used inodes (`-1`).
+   Display disk space in certain block sizes (`--block-size=<size>`).

# Checking Disk Usage with du

To find out how much space is being consumed by a particular directory (and its subdirectories), you can use the du command. With no options, du lists all directories below the current directory, along with the space consumed by each directory. At the end, du produces the total disk space used within that directory structure.

The du command is a good way to check how much space is being used by a particular user (du /home/user1) or in a particular file system partition (du /var). By default, disk space is displayed in 1-K block sizes. To make the output more friendly (in kilobytes, megabytes, and gigabytes), use the `-h` option as follows:

```
$ du -h /home/jake
114K    /home/jake/http/stuff
234K    /home/jake/http
137K    /home/jake/uucp/data
701K    /home/jake/uucp
1.0M    /home/jake
```

The output shows the disk space used in each directory under the home directory of the user named jake (/home/jake). Disk space consumed is shown in kilobytes (K) and megabytes (M). The total space consumed by /home/jake is shown in the last line. To avoid listing all the subdirectories and see a total for all files and directories below a certain directory, add the `-s` option as follows:

```
$ du -sh /home/jake
1.0M    /home/jake
```

# Finding Disk Consumption with find

The find command is a great way to find file consumption of your hard disk using a variety of criteria. You can get a good idea of where disk space can be recovered by finding files that are over a certain size or were created by a particular person.

> **NOTE** You must be the *root user* to run this command effectively, unless you are just checking your personal files.

In the following example, the *find* command searches the root file system (/) for any files owned by the user named jake (*-user jake*) and prints the filenames. The output of the *find* command is then listed with a long listing in size order (*ls -lds*). Finally, that output is sent to the file /tmp/jake. When you read the file /tmp/jake, you will find all of the files that are owned by the user jake, listed in size order. Here is the command line:

```
# find / -xdev -user jake -print | xargs ls -lds > /tmp/jake
```