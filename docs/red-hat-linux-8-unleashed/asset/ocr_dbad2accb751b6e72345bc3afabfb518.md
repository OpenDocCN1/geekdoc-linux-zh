# Granting System Administrator Privileges to Regular Users

By executing the following, you become that user and inherit the superuser-environment—a pretty handy tool. To become another user, specify a different user's name on the command line:

```
$ su - <some other user>
```

When leaving an identity to return to your usual identity, use the exit command. For example, while logged on as a regular user,

```
$ su root
```

the system prompts for a password:

Password:

When the password is entered correctly, the root user's prompt appears:

```
#
```

To return to the regular user's identity, just type

```
# exit
```

This takes you to the regular user's prompt:

```
$
```

If you need to allow other users access to certain commands with root privileges, it is necessary to give them the root password so that they can use su—that definitely isn't a secure solution. The next section describes a more flexible and secure method of allowing normal users to perform selected root tasks.

# Root Privileges on Occasion—The sudo Command

If it is desirable to give certain users only a few superuser permissions (to create an system administrator, for example), the sudo command is used. sudo (superuser) allows a regular user, after being given permission, the ability to use a superuser command. To use sudo, the user must authenticate himself with his password; he then can reuse the command for a specific period of time (five minutes by default) without further reauthentication. The list of authorized users is kept in /etc/sudoers, a file accessible only by root. If a user attempts to use a sudo command without authorization, that event is logged and a warning mail message could optionally be sent to the administrator.

To use sudo as a regular user, you prepend the command you are authorized to use the sudo command, for example,

```
$ sudo fdisk -l /dev/hda1
```