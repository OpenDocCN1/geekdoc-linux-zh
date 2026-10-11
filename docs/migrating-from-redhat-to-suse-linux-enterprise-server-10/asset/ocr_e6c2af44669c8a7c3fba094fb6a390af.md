+   * **/var/**. If the computer is used as a mail server, it might be a good idea to put /var/ on a separate partition. While too much mail might still render the mail service unusable, they would just fill the partition containing the /var directory, not the root file system. The administrator would still be able to administer the server and correct the issue.

+   * **/srv/**. When the machine acts as a web or ftp server, the data offered to users could be put on a separate partition.

+   * **/home/**. Putting /home/ on a separate partition prevents users from using up all disk space and facilitates updates. If you have to reinstall the operating system you can preserve data in /home by leaving the partition untouched.

+   * **/tmp/**. Having /tmp/ on a separate partition allows you to mount it with special options, like noexec, and also prevents processes from filling the disk with files in /tmp/.

+   * **Additional partitions.** If the partitioning is performed by YaST and other partitions are detected in the system, these partitions are also entered in the file /etc/fstab to enable easy access to this data.

The following is an example:

```
dev/sda8  /data2  auto  noauto,user  0  0
```

Such partitions, whether they are Linux or FAT, are specified by YaST with the options noauto and user. This allows any user to mount or unmount these partitions as needed.

For security reasons, YaST does not automatically enter the exec option, which is needed for executing programs from the respective location. However, you can enter this option manually.

Entering the exec option is necessary if you encounter system messages such as “bad interpreter” or “Permission denied”.