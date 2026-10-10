the `vi` editing commands found in Chapter 4 in the section “Working with `vi`.” You begin the editing by executing the `visudo` command with this:

```
# visudo
```

The default /etc/sudoers file looks like this:

```
# sudoers file.
#
#
# This file MUST be edited with the ‘visudo’ command as root.
#
# See the sudoers man page for the details on how to write a sudoers file.
#
# Host alias specification

# User alias specification

# Cmd alias specification

# Defaults specification

# User privilege specification
root   ALL=(ALL) ALL

# Uncomment to allow people in group wheel to run all commands
# %wheel ALL=(ALL) ALL

# Same thing without a password
# %wheel ALL=(ALL) NOPASSWD: ALL

# Samples
# %users ALL=/sbin/mount /cdrom,/sbin/umount /cdrom
# %users localhost=/sbin/shutdown -h now
```

The basic format of a sudoers line in the file is as follows:

```
user host_computer=command
```

The user can be an individual user or a group (prepended by a % to identify the name as a group). The host_computer is normally ALL for all hosts on the network and localhost for the local machine, but the host computer can be referenced as a subset of any specific host. The command in the sudoers line can be ALL, a list of specific commands, or a restric-tion on specific commands (formed by prepending a ! to the command). A number of