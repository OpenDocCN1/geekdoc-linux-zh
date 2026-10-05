# UNMOUNTING FILE SYSTEMS

The shutdown and reboot procedures unmount all file systems automatically. As part of this process, any file system data cached in memory is flushed to the storage device thus ensuring that the file system suffers no data corruption.

> WARNING File system data is cached in memory. Therefore, in order to avoid corrupting data on the disk, it is essential that you unmount removable drives before unplugging them. The unmount procedure synchronizes data before releasing the drive, ensuring data integrity.

To unmount a file system, the unmount command expects the mount point as argument.

```
[root@host ~]# unmount /mnt/data
```

Unmounting is not possible if the mounted file system is in use. The unmount command to succeed, all processes needs to stop accessing data under the mount point.

In the example below, the unmount fails because the file system is in use (the shell is using /mnt/data as its current working directory), generating an error message.

```
[root@host ~]# cd /mnt/data
[root@data]# unmount /mnt/data
unmount: /mnt/data: target is busy.
```

The lsof command lists all open files and the process accessing them in the provided directory. It is useful to identify which processes currently prevent the file system from successful unmounting.

| COMMAND PID USER FD TYPE DEVICE SIZE/OFF NODE NAME |
| bash | 1593 root | cwd | DIR 253,17 | 6 128 /mnt/data |
| lsof | 2532 root | cwd | DIR 253,17 | 19 128 /mnt/data |
| lsof | 2533 root | cwd | DIR 253,17 | 19 128 /mnt/data |

Once the processes are identified, an action can be taken, such as waiting for the process to complete or sending a SIGTERM or SIGKILL to the process. In this case, it is sufficient to change the current working directory to outside the mount point.

```
[root@data]# cd
[root@host ~]# unmount /mnt/data
```

> NOTE A common reason for file systems to fail to unmount is that a Bash shell is using the mount point or a subdirectories as a current working directory. Use the cd command to change out of the file system to resolve this problem.