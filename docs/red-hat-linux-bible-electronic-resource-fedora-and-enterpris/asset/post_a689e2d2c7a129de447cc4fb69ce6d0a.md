
```
tty:x:5:
disk:x:6:root
lp:x:7:daemon, lp
mem:x:8:
kmem:x:9:
wheel:x:10:root, joe, mary

nobody:x:99:
users:x:100:
chris:x:500
sheree:x:501
sales:x:601:bob, jane, joe, mary
```

Each line in the group file contains the name of a group, the group ID number associated with it, and a list of users in that group. By default, each user is added to his or her own group, beginning with GID 500. Note that mary was added to the wheel and sales groups instead of having her own group.

It is actually rather significant that mary was added to the wheel group. By doing this, you grant her the ability to use the sudo command to run commands as the root user (provided that sudo was configured as described in Chapter 10).

In this example, we used the -g option to assign mary to the users group. If you leave off the -g parameter, the default behavior is for useradd to create a new group with the same name and ID number as the user, which is assigned as the new user's primary group. For example, look at the following useradd command:

```
# useradd -m -G wheel, sales -s /bin/tcsh -c "Mary Smith" mary
```

It would result in a /etc/passwd line like this:

```
mary:x:502:502:Mary Smith:/home/mary:/bin/tcsh
```

It would also result in a new group line like this:

```
mary:x:502:
```

Note that the user ID and group ID fields now have the same number. If you set up all of your users this way, you will have a unique group for every user on the system, which allows for increased flexibility in the sharing of files among your users.

## Adding users with Red Hat User Manager

If you prefer a graphical window for adding, changing, and deleting user accounts, you can use the Red Hat User Manager window. To open the window from the GNOME desktop, click System Settings → Users and Groups (or type redhat-config-users from a Terminal window as root user). Figure 11-1 shows an example of that window.

![](img/27a85d56d393921ced6412ae6e8336bf_419_0.png)

Figure 11-1: Manage users from the Red Hat User Manager window.

When you open the Red Hat User Manager window, you see a list of all regular users that are currently added to your computer. Administrative users (UID 1 through 100) are not displayed. For each user, you can see the user name, UID, primary group, full name, login shell, and home directory. Click on any of those headings to sort the users by that information.

To add a new user from the Red Hat User Manager window, do the following:

- 1. Click the Add User icon. A Create New User window appears, as shown in Figure 11-2.

![](img/27a85d56d393921ced6412ae6e8336bf_419_1.png)

Figure 11-2: Create New User window.

- 2. Type the requested information in the following fields:

- **User Name** — A single word to describe the user. Typically, the user name is eight characters, all lowercase, containing the user’s real first name, last name, or (more often) a combination of the two (such as ijones).

- **Full Name** — The user’s full name (usually first name, middle initial, and last name). This name is typically just used for display, so using upper- and lowercase is fine.

- **Password** — The user’s initial password. (Ask the user to change this password the first time he or she logs in to the new account, using the passwd command.)
- **Confirm Password** — Type the password again, to make sure you entered it correctly.
- **Login Shell** — The default shell (for entering typed commands) that the user sees when first logging in to Red Hat Linux from a character display.
- **Create home directory** — By default, this box is selected and the user’s home directory (as indicated by the Home Directory field) is created automatically.
- **Home Directory** — By default, the user is given a home directory of the user’s name in the /home directory. (For example, the user sheree would be assigned /home/sheree as her home directory.) Change this field if you want to assign the user to a different home directory.
- **Create a private group for the user** — Check this box if you want a group by the same name as the user, created for this user. The name is added to the /etc/group file. This feature is referred to as user private groups (UPGs).

> TIP: Using UPGs can be a benefit for sharing a directory of files among several users. Here’s an example:
> 
> # useradd -m projectx
> # mkdir /usr/local/x
> # chown root.projectx /usr/local/x
> # chmod 2775 /usr/local/x
> # ls -ld /usr/local/x
> drwxrwsr-x 2 root projectx 4096 Aug 18 01:54 /usr/local/x
> # gpasswd -a nextuser projectx
> 
> In this example, you create a user named projectx (with a group named projectx). Create a /usr/local/x directory and have it owned by root user and projectx group. Set the setuid bit to be on for the group (2), open full read/write/execute permissions for user and group (77), and open read and execute permissions for everyone else (5). Add each user to the group that you want to be able to write to the projectx directory (replace nextuser with the user you want to add). After that, regardless of a user’s primary group, any file created in the /usr/local/x directory by a user will be read/writable by anyone in the projectx group.

- **Specify user ID manually** — Typically, you would not check this box, so that the UID for the new user would be assigned automatically. New UIDs for regular users start at 500. However, if you want to assign a particular UID for a user (for example, if you want to match the UID with the user’s UID from another computer on your network), click this box and type the number you want to use in the UID box.

- 3. Click OK when you are done. The new user is added to the /etc/passwd and /etc/group files. The user account is now available for that user to login.

## Setting User Defaults

The useradd command and Red Hat User Manager window both determine the default values for new accounts by reading the /etc/login.defs file. You can modify those defaults by either editing that file manually with a standard text editor or by running the useradd command with the -D option. If you choose to edit the file manually, here is what you face:

```
# *REQUIRED*
# Directory where mailboxes reside, _or_ name of file, relative to the
# home directory. If you_do_ define both, MAIL_DIR takes precedence.
# QMAIL_DIR is for Qmail
#
#QMAIL_DIR Maildir
MAIL_DIR    /var/spool/mail
#MAIL_FILE    .mail

# Password aging controls:
#
# PASS_MAX_DAYS    Maximum number of days a password may be used.
# PASS_MIN_DAYS    Minimum number of days allowed between password changes.
# PASS_MIN_LEN    Minimum acceptable password length.
# PASS_WARN_AGE    Number of days warning given before a password
#    expires.
#
PASS_MAX_DAYS        99999
PASS_MIN_DAYS        0
PASS_MIN_LEN        5
PASS_WARN_AGE        7


#
# Min/max values for automatic uid selection in useradd
#
UID_MIN                    500
UID_MAX                   60000

#
# Min/max values for automatic gid selection in groupadd
#
GID_MIN                    500
GID_MAX                   60000


#
# If defined, this command is run when removing a user.
# It should remove any at/cron/print jobs etc. owned by
# the user to be removed (passed as the first argument).
#
#USERDEL_CMD    /usr/sbin/userdel_local
```

```
#
# If useradd should create home directories for users by default.
# On RH systems, we do. This option is ORed with the -m flag on
# useradd command line.
CREATE_HOME yes
```

Blank lines and comments beginning with a pound sign (#) are ignored. All other lines contain keyword/value pairs. For example, the keyword MAIL_DIR is followed by some white space and the value /var/spool/mail. This tells useradd that the initial user e-mail mailbox is created in that directory. Following that are lines that enable you to customize the valid range of automatically assigned user ID numbers or group ID numbers. A comment section that explains that keyword’s purpose precedes each keyword. Altering a default value is as simple as editing the value associated with that keyword and then saving the login.defs file.

If you want to view the defaults, type the useradd command with the -D option as follows:

```
# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
```

You can also use the -D option to change defaults. When run with this flag, useradd refrains from actually creating a new user account; instead, it saves any additionally supplied options as the new default values in /etc/login.defs. Not all useradd options can be used in conjunction with the -D option. You may use only the five options listed in Table 11-2.

### Table 11-2: useradd Options for Changing User Defaults

| Options | Description |
| :--- | :--- |
| -b default_home | Set the default directory in which user home directories will be created. Replace default_home with the directory name to use. Usually this is /home. |
| -e default_expire_date | Set the default expiration date on which the user account is disabled. The default_expire_date value should be replaced with a date in the form MM/DD/YYYY — for example, 10/15/2001. |
| -f default_inactive | Set the number of days after a password has expired before the account is disabled. Replace default_inactive with a number representing the number of days. |
