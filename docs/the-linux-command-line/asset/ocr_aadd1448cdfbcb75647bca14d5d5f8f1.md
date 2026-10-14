```
```shell
[me@linuxbox ~]$ touch playground/timestamp
```
```

This creates an empty file named `timestamp` and sets its modification time to the current time. We can verify this by using another handy command, `stat`, which is a kind of souped-up version of `ls`. The `stat` command reveals all that the system understands about a file and its attributes:

```
```text
[me@linuxbox ~]$ stat playground/timestamp
  File: `playground/timestamp'
  Size: 0          Blocks: 0          IO Block: 4096 regular empty file
Device: 803h/2051d Inode: 14265061 Links: 1
Access: (0644/-rw-r--r--)  Uid: ( 1001/ me)   Gid: ( 1001/ me)
Access: 2008-10-08 15:15:39.000000000 -0400
Modify: 2008-10-08 15:15:39.000000000 -0400
Change: 2008-10-08 15:15:39.000000000 -0400
```
```

If we touch the file again and then examine it with `stat`, we will see that the file’s times have been updated:

```
```text
[me@linuxbox ~]$ touch playground/timestamp
[me@linuxbox ~]$ stat playground/timestamp
  File: `playground/timestamp'
  Size: 0          Blocks: 0          IO Block: 4096 regular empty file
Device: 803h/2051d Inode: 14265061 Links: 1
Access: (0644/-rw-r--r--)  Uid: ( 1001/ me)   Gid: ( 1001/ me)
Access: 2008-10-08 15:23:33.000000000 -0400
Modify: 2008-10-08 15:23:33.000000000 -0400
Change: 2008-10-08 15:23:33.000000000 -0400
```
```

Next, let’s use `find` to update some of our playground files:

```
```shell
[me@linuxbox ~]$ find playground -type f -name 'file-B' -exec touch
'{}' ';'
```
```

This updates all files in the playground named `file-B`. Next we’ll use `find` to identify the updated files by comparing all the files to the reference file `timestamp`:

```
```shell
[me@linuxbox ~]$ find playground -type f -newer playground/timestamp
```
```