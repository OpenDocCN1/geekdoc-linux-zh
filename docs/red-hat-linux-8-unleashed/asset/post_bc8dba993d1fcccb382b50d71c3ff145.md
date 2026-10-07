
8. The PATH defaults to /usr/local/bin:/bin:/usr/bin: for normal users and to /sbin:/bin:/usr/sbin:/usr/bin for root.

9. Normal greeting messages and mail checking are disabled if the file .hushlogin exists; otherwise, those messages are displayed at the end of the logon process.

10. The user's command shell is started at this point, presenting the user with a command prompt. If no shell is specified for the user in /etc/passwd, /bin/sh is used by default. (Unix operating systems will just log you back out.) If no home directory is specified in /etc/passwd, / is used.

When you log in as a regular user, the files that control your environment are found in your /home/username directory. These configuration files are naturally hidden from view; their filename is preceded by a period (as in .bashrc—these are known as 'dot files').

The name of the file indicates which program it is associated with. The files .bash_login, .bash_profile, and .bashrc determine how the bash shell is used by the user. (These files can, of course, be preset by the system administrator and the user given only read access so that they cannot be changed. Other shells have their own associated files.)

The .screenrc file determines the console environment, and the .Xdefaults file determines much the same thing for X11. For Red Hat, the .clients-default file is created by running the switchdex command to change the desktop for the user. You would use this if you occasionally launched X11 from the command line and desired to change your default desktop. Red Hat sets the default as GNOME.

Other files may be present depending on the system and the system administrator. The point is that the environment of each user can be set globally through the use of files in /etc/skel and individually by allowing user modification of the files in their /home directory (or not depending on the system administration policies).

The system logs all user logins, as well as all su and sudo commands for the admin's review. (The init, syslog, and klog applications create the logs.) Modern security monitoring programs (or simple scripts you create) can scan these files (such as /var/log/messages) for anomalies and signal possible security violations.

## Disk Quotas

On large systems with many users, you need to control the amount of disk space a user has access to. Disk quotas are designed for this purpose. Quotas, managed by each partition, can be set for both individual users as well as groups; quotas for the group need not be large as the quotas for the individuals in the groups.

When files are created, both a user and a group own them; ownership of the files is always part of the metadata about the files. This makes quotas based on both users and groups easy to manage.

### NOTE

Disk quota management is never done on a home system and rarely, if ever, done on a small office system.

To manage quotas you must have the quota software package installed on your system; it is not installed by default. Quota management with Red Hat Linux is not enabled by default and has traditionally been enabled and configured manually by system administrators. They use the family of Quota commands, such as edquota to set and edit user quotas, setquota to configure quotas, and quotaoff to control the service. (Other utilities include warnquota for automatically sending mail to users over their disk usage limit.)

## Implementing Quotas

To reiterate, quotas are not enabled by default, even if the quota software package is installed on your system. If installed and enabled, you can see which partitions have either user quotas, group quotas, or by looking at the fourth field in the /etc/fstab file. For example, one line in /etc/fstab shows that quotas are enabled for the /home partition:

```
/dev/hda5 /home ext3 defaults,usrquota,grpquota 1 1
```

The root of the partition will have the files quota.user or quota.group (or both types of quotas are enabled), and the files will contain the actual quotas. The permissions of these files should be 600 so that users cannot read or write to them. (Otherwise, users would change them to allow ample space for their music files and Internet art collections.) In order to initialize quotas, the partitions must be remounted. This is easily accomplished with the following:

```bash
# mount -o ro,remount <partition to be remounted>
```

The underlying console tools (complete with man pages) are:

- quotaon, quotaoff—Toggles quotas on a partition
- repquota—A summary status report on users and groups
- quotacheck—Updates the status of the quotas (compares new and old tables of disk usage); is run after fsck

## Manually Configuring Quotas

Manual configuration of quotas involves changing entries in your system's filesystem, /etc/fstab, to add the usrquota mount option to the desired partition of your file system.

## CHAPTER 9 Managing Users

As an example in a simple file system, quota management can be enabled by this:

```
LABEL=/                /ext3 defaults,usrquota 1 1
```

Group-level quotas can also be enabled by using the grquota option. As the root operator, you may create a file (using our example of creating user quotas) named quota.user in the designated portion of the file system, like so:

```bash
# touch /quota.user
```

You should then turn on the use of quotas using the quota command:

```bash
# quotaon
```

You can edit quotas with the edquota command:

```bash
# edquota -u username
```

You can set quotas with the setquota command:

```bash
# setquota -u username -b 100m -l 110m /home
```

You can check quotas with the quota command:

```bash
# quota -u username
```

You can turn off quotas with the quotaoff command:

```bash
# quotaoff -u username
```

## Related Red Hat Linux Commands

You'll use these commands to manage accounts:

- chage—Sets password expiration policies
- chgrp—Changes group ownership
- chmod—Changes file permissions
- chown—Changes file ownership
- chpasswd—Changes passwords
- chsh—Modifies shell
- groups—Displays group memberships
- logname—Displays login name
- newusers—Creates users
- passwd—Changes passwords
- redhat-config—User management
- su—Executes shell as another user
- sudo—Manages selected execution

### Reference

- useradd—Creates, modifies, or manages users
- userinfo—Displays user information
- usermod—Edits a user
- userdel—Deletes users
