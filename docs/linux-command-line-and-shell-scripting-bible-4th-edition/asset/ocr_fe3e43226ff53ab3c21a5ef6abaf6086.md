h, which shows the disk space in human-readable form, usually as an M for megabytes or a G for gigabytes:

```
$ df -h
Filesystem     Size  Used Avail Use% Mounted on
/dev/sda5        19G  7.0G   11G  40% /
/dev/sda2       512M  4.0K  512M   1% /boot/efi
/dev/sdb1        961M  242M  720M  26% /media/rich/54A1-7D7D
$ 
```

Now instead of having to decode those ugly block numbers, all of the disk sizes are shown using “normal” sizes. The df command is invaluable in troubleshooting disk space problems on the system.

> **NOTE**
> 
> Remember that the Linux system always has processes that handle files running in the background. The values from the df command reflect what the Linux system thinks are the current values at that point in time. It’s possible that you have a process running that has created or deleted a file but has not released the file yet. This value is not included in the free space calculation.

# Using the du command

With the df command, it is easy to see when a disk is running out of space. The next problem for the system administrator is to know what to do when that happens.

Another useful command to help you out is the du command. The du command shows the disk usage for a specific directory (by default, the current directory). This is a quick way to determine if you have any obvious disk hogs on the system.

By default, the du command displays all the files, directories, and subdirectories under the current directory, and it shows how many disk blocks each file or directory takes. For a standard-sized directory, this can be quite a listing. Here’s a partial listing of using the du