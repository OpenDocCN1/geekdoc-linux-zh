the edquota command. For example, to allocate a disk quota for a user named kabir, run edquota as follows:

```
edquota -u kabir
```

This brings up the default text editor (such as vi or whatever editor is set in the $EDITOR environment variable) with contents similar to the following:

```
Quotas for user kabir:
/dev/sda5: blocks in use: 0, limits (soft = 0, hard = 0)
    inodes in use: 0, limits (soft = 0, hard = 0)
```

Here, the user kabir has so far used 0 blocks (in K) on disk partition /dev/sda5 (under usrquota control), and the limits (soft or hard) are not set yet. Similarly, this user has not yet owned any files (inodes), and no limit (soft or hard) has been set yet.

As you can see, you can simultaneously set limits for the amount of space (in blocks) a user can consume and control how many files can be owned by the user. The soft limit specifies the maximum amount of disk space (blocks) or files (inodes) a user can have on the file system. The hard limit is the absolute amount of disk space (in blocks) or files (inodes) a user can have.

For example, suppose you want to allow user kabir to have a soft limit of 1MB (1,024K) and a hard limit of 4MB (4,096K) for disk space. Also, suppose that you want to allow this user a soft limit of 128 files/directories (inodes) and a hard limit of 512 files/directories. Set the quota limit using edquota -u kabir as follows:

```
Quotas for user kabir:
/dev/sda5: blocks in use: 0, limits (soft = 1024, hard = 4096)
    inodes in use: 0, limits (soft = 128, hard = 512)
```

After you save the configuration, the user can no longer exceed the hard limits. If the user tries to go over any of these two (disk space and inode count) limits, an error message will be displayed. For example, in the following, user kabir tries to create a new directory in /home, but the quota limit for this quota has been exceeded, so the error message is displayed:

```
[kabir@picasso /home]$ mkdir eat_space
mkdir: cannot make directory `eat_space': Disc quota exceeded
```