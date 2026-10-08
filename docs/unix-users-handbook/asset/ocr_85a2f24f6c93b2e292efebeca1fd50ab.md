# **tar**

**tar** is the most popular generic backup utility. You will find that many applications are shipped on **tar** tapes. This is the most widely used format for exchanging data with other UNIX systems. **tar** is the oldest UNIX backup method and therefore runs on all UNIX systems. You can append files to the end of a **tar** tape. When sending files to another UNIX user, I would strongly recommend **tar**. **tar** is as slow as molasses, so you won't want to use it for your full or incremental backups. One highly desirable aspect of **tar** is that when you load files onto a tape with **tar** and then restore them onto another system, the original users and groups are retained. For instance, to back up all files belonging to frank and load them onto another system, you would use the following commands:

```
$ cd /home/frank

$ tar -cvf /dev/rmt/0m .
```

The **c** option creates a new **tar** file, the **v** option produces a verbose output, and the **f** option indicates the file or device to be used for the backup, which is the device file /dev/rmt/0m. The dot indicates that the backup will start in the present working directory. You could then load frank's files on another system even if the user frank and his group don't yet exist on that system.

# **cpio**

**cpio** is also portable and easy to use, like **tar**. In addition, **cpio** is much faster than **tar**. **cpio** is good for replicating directory trees. **cpio** supports the incremental backup discussed earlier. You simply give **cpio** a list of files and it will perform a backup.