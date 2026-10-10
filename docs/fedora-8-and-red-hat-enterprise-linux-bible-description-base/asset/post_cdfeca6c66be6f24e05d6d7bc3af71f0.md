
## Figure 11-1: Manage users from the User Manager window.

![Figure 11-1](img/fb202c163797a743c3c6cf236316bc96_508_0.png)

To add a new user from the User Manager window, do the following:

- Click the Add User icon to open the Create New User window (see Figure 11-2).

![Figure 11-2](img/fb202c163797a743c3c6cf236316bc96_508_1.png)

**Figure 11-2: The Create New User window**

- Type the requested information in the following fields:
    - **User Name** — A single word to describe the user. Typically, the user name is eight characters, all lowercase, containing the user’s real first name, last name, or (more often) a combination of the two (such as jjones).
    - **Full Name** — The user’s full name (usually first name, middle initial, and last name). This name is typically just used for display, so using upper- and lowercase is fine.
    - **Password** — The user’s initial password. (Ask the user to change this password the first time he or she logs in to the new account, using the `passwd` command.)
    - **Confirm Password** — Type the password again, to make sure you entered it correctly.
    - **Login Shell** — The default shell (for entering typed commands) that the user sees when first logging in to Fedora or RHEL from a character display.
    - **Create home directory** — By default, this box is selected and the user’s home directory (as indicated by the Home Directory field) is created automatically.
    - **Home Directory** — By default, the user is given a home directory of the user’s name in the `/home` directory. (For example, the user *sheree* would be assigned `/home/sheree` as her home directory.) Change this field if you want to assign the user to a different home directory.
    - **Create a private group for the user** — Check this box if you want a group by the same name as the user, created for this user. The name is added to the `/etc/group` file. This feature is referred to as user private groups (UPGs).
    - **Specify user ID manually** — Typically, you would not check this box, so that the UID for the new user would be assigned automatically. New UIDs for regular users start at 500. However, if you want to assign a particular UID for a user (for example, if you want to match the UID with the user’s UID from another computer on your network), select this box and type the number you want to use in the UID box.
    - **Specify group ID manually** — As with the user ID, you would typically just have the group ID automatically assigned. However, you can assign a different GID to have the user assigned to a particular group.
- Click OK when you are done. The new user is added to the `/etc/passwd` and `/etc/group` files. The user account is now available for that user to log in.

**TIP:** Using user private groups (UPGs) can be a benefit for sharing a directory of files among several users. Here’s an example:

```bash
# useradd -m projectx
# mkdir /usr/local/x
# chown root.projectx /usr/local/x
# chmod 2775 /usr/local/x
# ls -ld /usr/local/x
drwxrwsr-x 2 root projectx 4096 Aug 18 01:54 /usr/local/x
# gpasswd -a nextuser projectx
```

In this example, you create a user named `projectx` (with a group named `projectx`). Create a `/usr/local/x` directory and have it owned by root user and `projectx` group. Set the setgid bit to be on for the group (2), open full read/write/execute permissions for user and group (77), and open read and execute permissions for everyone else (5). Add each user to the group that you want to be able to write to the `project` directory (replace `nextuser` with the user you want to add). After that, regardless of a user's primary group, any file created in the `/usr/local/x` directory by a user can be read or modified by anyone in the `projectx` group.

## Setting User Defaults

The `useradd` command and User Manager window both determine the default values for new accounts by reading the `/etc/login.defs` file. You can modify those defaults by either editing that file manually with a standard text editor or by running the `useradd` command with the `-D` option. If you choose to edit the file manually, here is what you face:

```text
# *REQUIRED*
# Directory where mailboxes reside, or name of file, relative to the
# home directory. If you define both, MAIL_DIR takes precedence.
# QMAIL_DIR is for Qmail
#
#QMAIL_DIR Maildir
MAIL_DIR       /var/spool/mail
#MAIL_FILE .mail

# Password aging controls:
#
# PASS_MAX_DAYS Maximum number of days a password may be used.
# PASS_MIN_DAYS Minimum number of days allowed between password changes.
# PASS_MIN_LEN Minimum acceptable password length.
# PASS_WARN_AGE Number of days warning given before a password
# expires.

PASS_MAX_DAYS  99999
PASS_MIN_DAYS  0
PASS_MIN_LEN   5
PASS_WARN_AGE  7

#
# Min/max values for automatic uid selection in useradd
#
UID_MIN        500
UID_MAX        60000

#
# Min/max values for automatic gid selection in groupadd
#
GID_MIN        500
GID_MAX        60000

#
# If defined, this command is run when removing a user.
# It should remove any at/cron/print jobs etc. owned by
# the user to be removed (passed as the first argument).
#
#USERDEL_CMD /usr/sbin/userdel_local

#
# If useradd should create home directories for users by default.
# On RH systems, we do.  This option is overridden with the -m flag on
# useradd command line.

CREATE_HOME yes
# The permission mask is initialized to this value. If not
# specified, the permission mask will be initialized to 022.
UMASK            077

# This enables userdel to remove groups if no members exist.
#
USERGROUPS_ENAB yes
# Use MD5 or DES to encrypt password? RedHat use MD5 by default.
MD5_CRYPT_ENAB yes
```

Blank lines and comments beginning with a pound sign (#) are ignored. All other lines contain keyword/value pairs. For example, the keyword MAIL_DIR is followed by some white space and the value /var/spool/mail. This tells useradd that the initial user e-mail mailbox is created in that directory. Following that are lines that enable you to customize the valid range of automatically assigned user ID numbers or group ID numbers. A comment section that explains that keyword’s purpose precedes each keyword. Altering a default value is as simple as editing the value associated with that keyword and then saving the login.defs file.

If you want to view the defaults, type the useradd command with the -D option as follows:

```bash
# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKELE=/etc/skel
CREATE_MAIL_SPOOL=yes
```

You can also use the -D option to change defaults. When run with this flag, useradd refrains from actually creating a new user account; instead, it saves any additionally supplied options as the new default values in /etc/login.defs. Not all useradd options can be used in conjunction with the -D option. You can use only the five options listed in Table 11-2.

**Table 11-2: useradd Options for Changing User Defaults**

| Options | Description |
| :-- | :-- |
| -b default_home | Set the default directory in which user home directories will be created. Replace default_home with the directory name to use. Usually this is /home. |
| -e default_expire_date | Set the default expiration date on which the user account is disabled. The default_expire_date value should be replaced with a date in the form MM/DD/YYYY—for example, 10/15/2007. |
| -f default_inactive | Set the number of days after a password has expired before the account is disabled. Replace default_inactive with a number representing the number of days. |
| -g default_group | Set the default group that new users will be placed in. In Fedora, useradd creates a new group with the same name and ID number as the user, so this value is ignored. To set a different group primary group for a user, you must set it explicitly with the -g option on the command line. |
| -s default_shell | Set the default shell for new users. Typically this is /bin/bash. Replace default_shell with the full path to the shell that you want as the default for new users. |

To set any of the defaults, give the -D option first; then add any of the defaults you want to set. For example, to set the default home directory location to /home/everyone and the default shell to /bin/tcsh, type the following:

```bash
# useradd -D -b /home/everyone -s /bin/tcsh
```

Besides setting up user defaults, an administrator can create default files that are copied to each user’s home directory for use. These files can include login scripts and shell configuration files (such as .bashrc). The following sections describe some of these files.

### Supplying initial login scripts

Many Linux applications, including the command shell itself, read a configuration file at startup. It is traditional practice that these configuration files are stored in the users’ home directories. In this way, each user can customize the behavior of the command shell and other applications without affecting that behavior for other users. In this way, global defaults can be assigned from /etc/profile, and then those settings can be enhanced by a user’s personal files.

The bash command shell, for example, looks for a file called .bashrc in the current user’s home directory whenever it starts up. Similarly, the tcsh command shell looks for a file
