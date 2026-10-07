# Disk Quotas 27

NOTE

Disk quota management is never done on a home system and rarely, if ever, done on a small office system.

To manage quotas you must have the quota software package installed on your system; it is not installed by default. Quota management with Red Hat Linux is not enabled by default and has traditionally enabled and configured manually by system administrators. They use the family of Quota commands, such as edquota to set and edit user quotas, setquota to configure quotas, and quotaoff to control the service. (Other utilities include warnquota for automatically sending mail to users over their disks usage limit.)

# Implementing Quotas

To reiterate, quotas are not enabled by default, even if the quota software package is installed on your system. If installed and enabled, you can see which partitions have either user quotas, group quotas, or by looking at the fourth field in the /etc/fstab file. For example, one line in /etc/fstab shows that quotas are enabled for the /home partition:

```
/dev/hda5 /home ext3 defaults,usrquota,grpquota 1 1
```

The root of the partition will have the files quota.user or quota.group (or both types of quotas are enabled), and the files will contain the actual quotas. The permissions of these files should be 600 so that users cannot read or write to them. (Otherwise, users would change them to allow ample space for their music files and Internet art collections.) In order to initialize quotas, the partitions must be remounted. This is easily accomplished with the following:

```
# mount -o ro,remount <partition to be remounted>
```

The underlying console tools (complete with man pages) are

+   - quotaon, quotaoff—Toggles quotas on a partition
- repquota—A summary status report on users and groups
- quotacheck—Updates the status of the quotas (compares new and old tables of disk usage); is run after fsck

# Manually Configuring Quotas

Manual configuration of quotas involves changing entries in your system's filesystem, /etc/fstab, to add the usrquota mount option to the desired partition of your file