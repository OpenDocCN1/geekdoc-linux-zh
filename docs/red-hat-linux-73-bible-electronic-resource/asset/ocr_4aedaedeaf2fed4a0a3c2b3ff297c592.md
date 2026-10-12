Turn on the quota startup script. If you created a quota file, as described in the previous step, you need to make it executable and set it to start automatically when you start Red Hat Linux. To do those things, type the following as root user:

```
# chmod 755 /etc/init.d/quota
# chkconfig on quota
```

At this point, links are created so that your quota script starts when Red Hat Linux boots.

# ## Creating quota rules

You can use the edquota command to create quota rules for a particular user or group. (Valid users and groups are listed in the /etc/passwd and /etc/group files, respectively.) Here is an example of an edquota command to set quotas for a user named jake.

> NOTE: The edquota command uses the vi text editor to edit your quota files. To use a different editor, change the value of the EDITOR or VISUAL environment variable before running edquota. For example, to use the emacs editor, type the following before running edquota:
> # export EDITOR=emacs

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

This example shows that user quotas can be set for the user jake on the /dev/hda2 partition (which is /home in our example). Currently, jake has used 596 blocks (a block equals 1K on this ext3 file system). One file was created by jake (represented by 1 inode). To change the disk usage limits, you can edit the zeros (unlimited use) under the soft and hard heading for blocks and inodes.

Soft limits set limits that you don't want a user or group to exceed. Hard limits set the boundaries that you will not let a user or group exceed. After a set grace period that a soft limit is exceeded (which is seven days, by default), the soft limit becomes a hard limit. (Type edquota -t to check and change the grace periods that you have set.)

Here is an example of how the line in the previous edquota example could be changed:

```
/dev/hda2 596 512000 716800 1 800 1000
```

In this example, the soft limit on the number of blocks that the user jake could consume on the /dev/hda2 device (/home) is 512000 blocks (or 500MB) the hard limit is 716800 blocks