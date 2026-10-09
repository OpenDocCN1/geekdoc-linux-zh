# SECURITY

The /etc/sudoers file configuration can give a user full root privileges or just access to specific programs. The previous entry allows jsmith full access to any root program. The result can be seen in Figure 12-5. Here jsmith tries to create a directory from the root directory and permission is denied. But with the sudo command, jsmith can issue the same command and the directory is created. The password entered is jsmith's password.

# FIGURE 12-5
Using the sudo command.

```
```
jsmith@style:
login as: jsmith
Sent username 'jsmith'
jSmith@192.168.0.21's password:
$ mkdir /jSmith
mkdir: cannot create directory '/jSmith': Permission denied
$ sudo mkdir /jSmith
Password:
```

```

# NOTE

An additional advantage of using sudo is that all commands executed via sudo are logged to the log file /var/log/secure. This is sometimes very useful to system administrators.

The /etc/sudoers file can be fine-tuned to enable specific users to access specific re-stricted programs. For example, to give user dengle permission to start or stop sendmail, add the following lines to the file (Figure 12-6):

```
```
dengle ALL=/sbin/service sendmail stop
dengle ALL=/sbin/service sendmail start
```

```

# FIGURE 12-6
/etc/sudoers file with single-user entry.

```
```
root@linux:
# sudoers file.
#
# This file MUST be edited with the 'visudo' command as root.
#
# See the sudoers man page for the details on how to write a sudoers file.
#
# Host alias specification
# User alias specification
# Cmd alias specification
# Defaults specification
# User privilege specification
root	ALL=(ALL) ALL
jSmith	ALL=(ALL) ALL
dengle	ALL=/sbin/service sendmail stop
dengle	ALL=/sbin/service sendmail start
# Uncomment to allow people in group wheel to run all commands
#wheel	ALL=(ALL)	ALL
# Same thing without a password
#%wheel	ALL=(ALL)	NOPASSWD: ALL
# Samples
# %users	ALL=/sbin/umount /cdrom,/sbin/umount /cdrom
# %users localhost=/sbin/shutdown -h now
```

```