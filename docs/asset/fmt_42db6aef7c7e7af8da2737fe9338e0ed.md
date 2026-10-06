
## 412 Part III: Administering Red Hat Linux

### Chapter 11: Setting Up and Supporting Users 413

## Deleting user accounts with Red Hat User Manager

Delete a user from the Red Hat User Manager window, simply click on the line representing the user account, then click the Delete button. The result of this action is:

- The information about the user is removed from the `/etc/passwd` file, the user can no longer log in.
- The home directory and all files owned by the user will still exist. However, a listing of files previously owned by that (`ls -1`) will only show the owner as the former user's UID, but no name.

See the description in the previous section for information about how to find and remove files previously owned by the user.

> TIP: You may want to transfer the ownership of the files from the old user to the new user. For example, if a new employee is taking over the work of an employee who is leaving the company. In that case, after you delete the old user, you can create a new user account, using the same UID as the old account (with a new password, of course). The new user will immediately have ownership of all files owned by the deleted user.

## Checking Disk Quotas

Limited disk space can be another source of user support calls. Red Hat Linux offers the quota software package for limiting and displaying disk space that a user can consume. You can use the `du` command to see how much disk space has been used in a particular directory (and related subdirectories). To automate the process of checking for disk space, you can create your own script. The following sections describe these ways of dealing with potential disk space problems.

## Using quota to check disk usage

A careless or greedy user has the potential of gobbling up all the space on your hard disk and possibly, bringing your computer to a halt. By using disk quotas, you can limit the amount of disk resources a user or group can use.

The quota package contains a set of tools that lets you limit the amount of disk space (based on disk blocks) and files (based on inodes) that a user can consume. Using quotas, you can limit the amount of usage (on a per-user and -group basis) for each file system on your computer. The general steps for setting disk quotas are:

- Creating quota files
- Editing the `/etc/fstab` file
- Creating quota rules
- Checking quotas

## 414 Part III: Administering Red Hat Linux

You set quotas on disk partitions listed in your `/etc/fstab` file. For computers that are shared by many users, there may be a separate `/home` or `/var` partition where users are expected to put all their data. That kind of partition boundary can prevent an entire disk being consumed by one user. Quotas on the `/home` or `/var` partition can make sure that the state within those partitions is fairly among your computer's users.

The procedure that spans the next few sections assumes that you have a separate `/home` partition on your computer for which you want to create quotas. You could use any partition, not just the `/home` partition shown in the procedure. For example, if you have only one partition mounted at the root of the files system (`/`), you could set quotas for your entire system by replacing `/home` with `/` in the following example.

## Creating quota files

You need to have `aquota.user` and/or `aquota.group` files in the root directory of the partition on which you want to establish disk quotas. To add quotas based on individual users, you need an `aquota.user` file, while `aquota.group` is needed to set quotas based on groups. One way to create these files is with the `quotaocheck` command. Here is an example of the `quotaocheck` command:

```
# quotaocheck -vug /home
```

The `quotaocheck` command in this example looks at the file system partition mounted on `/home` and builds a table of disk usage. The `-v` option produces verbose output from the command, the `-u` option causes quotas to be examined, and the `-g` option causes group quotas to be examined. Because of them, the `aquota.user` and `aquota.group` files are created in the root directory.

## Editing /etc/fstab

查看挂载在 `/home` 上的文件系统分区并构建磁盘使用表。为了，编辑 `/etc/fstab` 文件并添加以下行（此处重复逻辑）。这里是 `quotaocheck` 命令的示例：

```
# quotaocheck -vug /home
```

（注：由于原文文本在后部分出现了严重的重复和逻辑错乱，译文已根据文档工程师逻辑对重复内容进行了翻译，并保持了原文的结构标记。）
