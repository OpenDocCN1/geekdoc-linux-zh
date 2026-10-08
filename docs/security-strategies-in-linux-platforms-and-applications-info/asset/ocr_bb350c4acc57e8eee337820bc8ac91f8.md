Just remember, the use of such passwords can be a security risk. Because the root administrative password is all-powerful for a system, it should be shared with as few people as possible. In addition, if you send an administrative password over a network, that's a risk, even over an encrypted connection. That's one reason for the sudo command, configured in the /etc/sudoers file.

# Options with sudo and /etc/sudoers

The Linux way to configure limited administrative permissions is based on the sudo command, configured in the /etc/sudoers configuration file. With sudo, authorized users need only to enter their regular passwords to run configured administrative commands. In the following, you'll look at basic options in /etc/sudoers, take a more extensive view of the commands that can be delegated through /etc/sudoers, and see how the sudo command works with this file.
The sudo command is so important in the Ubuntu distribution that you won't even find a root administrative password on Ubuntu releases. The first user on an Ubuntu system is given membership in the admin group. A regular user who is a member of the admin group can run administrative commands with full privileges (if that group is appropriately configured in /etc/sudoers). As described later, all that user needs to do is enter his or her own password when prompted.

> NOTE
it is possible to log into the root account in Ubuntu. You can boot a system into the recovery mode normally configured in the Grand Unified Bootloader (GRUB) menu described in Chapter 3. Alternatively, if your account is configured with appropriate privileges, you can run the sudo command. Once in the root account, you can activate logins to that account by creating a password. The passwd command in the root account makes it easy.

# Basic Options in /etc/sudoers

The standard /etc/sudoers file contains the following entry, which gives the root administrative user full privileges through sudo:

```
root ALL=( ) ALL
```

The format of this line is as follows (if run_as_username is not included, it's assumed that the command that runs is as root):

```
user system=run_as_username command
```

The user can be any regular user account in /etc/passwd. Alternatively, a name with a % in front specifies a group. So the following entries full administrative privileges for members of the admin group:

```
%admin ALL=( ) ALL
```