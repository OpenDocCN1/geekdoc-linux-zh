
You set quotas on disk partitions listed in your `/etc/fstab` file. For computers that are shared by many users, there may be a separate `/home` or `/var` partition where users are expected to put all their data. That kind of partition boundary can prevent an entire disk being consumed by one user. Quotas on the `/home` or `/var` partition can make sure that the space within those partitions are shared fairly among your computer's users.

The procedure that spans the next few sections assumes that you have a separate `/home` partition on your computer for which you want to create quotas. You could use any partition, not just the `/home` partition shown in the procedure. For example, if you have only one partition mounted at the root of the file system (/), you could set quotas for your entire file system by replacing `/home` with `/` in the following example.

## Creating quota files

You need to have `aquota.user` and/or `aquota.group` files in the root directory of the partition on which you want to establish disk quotas. To add quotas based on individual users, you need an `aquota.user` file, while `aquota.group` is needed to set quotas based on groups. One way to create these files is with the **quotacheck** command. Here is an example of the quotacheck command:

```
# quotacheck -vug /home
```

The quotacheck command in this example looks at the file system partition mounted on `/home` and builds a table of disk usage. The `-v` option produces verbose output from the command, the `u` option causes user quotas to be examined, and the `g` option causes group quotas to be examined. Because the quota files don't exist yet, the command creates them (`aquota.user` and `aquota.group`) in the `/home` directory. Permissions on the two files are set so only root can access them (`chmod 600 aquota.*`).

## Editing /etc/fstab file

You need to add quota support to the file system. To do that, edit the `/etc/fstab` file and add the `usrquota` option to field number four of the partition for which you want to set quotas. Here is an example of a line from `/etc/fstab`:

```
/dev/hda2      /home      ext3      defaults,usrquota,grpquota      1 2
```

In this example, the `/home` file system is being used to allow disk quotas for all users' home directories under the `/home` directory.

Before the `usrquota` option can take effect, the file system must be remounted. This happens automatically when you reboot, which you will have to do if you are setting quotas for the root (/) file system. Otherwise, you might be able to use the `umount` and `mount` commands to cause the `usrquota` option to take effect.

## Creating a quota startup script

If the quota package doesn't include a startup script (and it doesn't with Red Hat Linux 7.3), you can create your own. You want this script to check quotas (`quotacheck` command), start the quota service (`quotaon` command) and turn off the service (`quotaoff` command).

Open a new file called `/etc/init.d/quota` as root user, using any text editor. Here is an example of the content you can add to that file:

```bash
#!/bin/bash
# init file for quota
#
# description: Checks disk quotas
#
# processname: quota
# chkconfig: - 90 90
# source function library
. /etc/rc.d/init.d/functions

case "$1" in
  start)
    echo -n "Checking quotas: "
    daemon /sbin/quotacheck -avug
    echo
    echo -n "Starting quotas: "
    daemon /sbin/quotaon -avug
    echo
  ;;
  stop)
    echo -n "Shutting down quotas: "
    daemon /sbin/quotaoff -a
    echo
  ;;
  restart)
    $0 stop
    $0 start
  ;;
  *)
    echo "Usage: quota {start|stop|restart}"
    exit 1
esac

exit 0
```

The quota script, when started, first runs the `quotacheck` command to check all file systems for which quota checking is available. Then it turns on quota checking with the `quotaon` command.

Turn on the quota startup script. If you created a quota file, as described in the previous step, you need to make it executable and set it to start automatically when you start Red Hat Linux. To do those things, type the following as root user:

```
# chmod 755 /etc/init.d/quota
# chkconfig on quota
```

At this point, links are created so that your quota script starts when Red Hat Linux boots.

## Creating quota rules

You can use the `edquota` command to create quota rules for a particular user or group. (Valid users and groups are listed in the /etc/passwd and /etc/group files, respectively.) Here is an example of an `edquota` command to set quotas for a user named jake.

> **NOTE:** The `edquota` command uses the `vi` text editor to edit your quota files. To use a different editor, change the value of the `EDITOR` or `VISUAL` environment variable before running `edquota`. For example, to use the `emacs` editor, type the following before running `edquota`:
> `# export EDITOR=emacs`

```
# edquota -u jake
Disk quotas for user jake (uid 501)
Filesystem blocks soft hard inodes soft hard
/dev/hda2 596 0 0 1 0 0
~
~
~
~
~
"/tmp/EdgP.aBylzYC" 3L, 215C
```

This example shows that user quotas can be set for the user jake on the `/dev/hda2` partition (which is `/home` in our example). Currently, jake has used 596 blocks (a block equals 1K on this ext3 file system). One file was created by jake (represented by 1 inode). To change the disk usage limits, you can edit the zeros (unlimited use) under the soft and hard heading for blocks and inodes.

Soft limits set limits that you don't want a user or group to exceed. Hard limits set the boundaries that you will not let a user or group exceed. After a set grace period that a soft limit is exceeded (which is seven days, by default), the soft limit becomes a hard limit. (Type `edquota -t` to check and change the grace periods that you have set.)

Here is an example of how the line in the previous `edquota` example could be changed:

```
/dev/hda2 596 512000 716800 1 800 1000
```

In this example, the soft limit on the number of blocks that the user jake could consume on the `/dev/hda2` device (`/home`) is 512000 blocks (or 500MB), the hard limit is 716800 blocks (or 700MB). Soft and hard limits on inodes are 800 and 1000, respectively. If either of the soft limits are exceeded by the user *jake*, he has seven days to get back under the limit, or he will be blocked from using any more disk space or inodes.

Further attempts to write to a partition after the hard limit has been exceeded results in a failure to write to the disk. When this happens, the user that tries to create the file that exceeds his limit will see a message like the following:

```
ide0(3,2): write failed, user block limit reached.
cp: writing 'abc.doc': Disk quota exceeded
```

Instead of assigning quotas to users, you can assign quotas to any group listed in the `/etc/group` file. Instead of the `-u` option to `edquota`, use the `-g` options followed by a group name.

## Updating quota settings

After you have changed quota settings for a user, you should rerun the **quotacheck** command. You should also run the **quotacheck** command periodically, to keep the quota records up to date. One way to do that is to run the **quotacheck** command weekly using a cron entry.

## Checking quotas

To report on how much disk space and how many inodes each user on your computer (for which you have set quotas) has consumed, use the **repquota** command. Here is an example of the **repquota** command for reading quota data relating to all partitions that are using quotas:

| | | used | soft | hard | grace | used | soft | hard | grace |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| **User** | | | | | | **Block limits** | | | |
| root | -- | 1973984 | 0 | 0 | | 2506 | 0 | 0 | |
| jake | -- | 1296 | 700 | 1700 | 6days | 3 | 0 | 0 | |

In this previous example, *jake* has exceeded his soft limit of 700 blocks. He currently has six days left in his grace period to remove enough files so that the soft limit does not become the hard limit.

## Using du to check disk use

You can discover the most voracious consumers of disk space using the **du** command. Invoke `du` with the `-s` option and give it a list of directories; it reports the total amount of disk space used by all the files in each directory. You can thus use the **du** command to list the total disk space used by each subdirectory within the `/home` directory. Try the following:

```
# du -s /home/*
```
