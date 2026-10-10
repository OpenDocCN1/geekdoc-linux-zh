The quota package contains a set of tools that lets you limit the amount of disk space (based on disk blocks) and files (based on inodes) that a user can consume. Using quotas, you can limit the amount of usage (on a per-user and per-group basis) for each file system on your computer. The general steps for setting disk quotas are:

+   1.  Edit the `/etc/fstab` file.
+   2.  Create quota files.
+   3.  Create and start a quota startup script.
+   4.  Create quota rules.
+   5.  Check quotas.

You set quotas on file systems listed in your `/etc/fstab` file. For computers that are shared by many users, there might be a separate `/home` or `/var` partition where users are expected to put all their data. That kind of partition boundary can prevent an entire disk from being consumed by one user. Quotas on the `/home` or `/var` partition can make sure that the space within those partitions is shared fairly among your computer's users.

> **NOTE:** When you begin setting user disk quotas, keep track of the total amount of disk space that can be consumed by the users you assign. Although quotas can limit how much each user can consume, they don't prevent your system from running out of disk space when the total amount of disk space allocated exceeds the total amount available.

The procedure that spans the next few sections assumes that you have a separate `/home` partition on your computer for which you want to create quotas. You could use any partition, not just the `/home` partition shown in the procedure. For example, if you have only one partition mounted at the root of the file system (`/`), you could set quotas for your entire file system by replacing `/home` with `/` in the following example.

# **Editing the `/etc/fstab` file**

To add quota support to the file system, edit the `/etc/fstab` file and add the `usrquota` option to field number four of the partition for which you want to set quotas. Here is an example of a line from `/etc/fstab`:

```
```text
/dev/sda2 /home ext3 defaults,usrquota,grpquota 1 2
```
```

Here, the `/home` file system is used to allow disk quotas for all users' home directories under the `/home` directory.

Before the `usrquota` option can take effect, the file system must be remounted. This happens automatically when you reboot, which you will have to do if you are setting quotas for the root (`/`) file system. Otherwise, you might be able to use the `umount` and `mount` commands to cause the `usrquota` option to take effect, or run `mount` with the `remount` option.