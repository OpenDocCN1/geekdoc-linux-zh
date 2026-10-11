
Even if a field is blank, it still needs to be defined by a colon (**:****). For example, the record for the user account `mail` ends in a colon because no login command is defined for this user. This same format is used on almost all UNIX systems.

## Key Concept

Each line in the `/etc/passwd` file must contain seven fields. Although some of these fields might be blank, they still need to be defined by colons.

### Username Field

The first field is the username. It must be unique to the system. It is usually eight characters or less and can contain letters, numbers, underscores, periods, and some special characters. However, the use of non-alphanumeric characters can lead to problems with some applications. In addition, usernames are case sensitive, so the usernames `thadden` and `Thadden` are two different users.

Because usernames are used for many purposes including `mail` and must be unique to your system, you need to consider how you are going to assign usernames. If you have only a few users on your system, it is not as important to be consistent with usernames. However, when a system is larger, it becomes too difficult to figure out just who a user is if there is not a logical method of assigning usernames.

One method of naming users is by using a combination of the first initial and part or all of the last name. So, a user by the name of Theresa Hadden would be given a username of `thadden`. Another combination could be first name and last initial, such as `therasah`. Be consistent in whatever method you decide to use.

### Password Field

The next field in each record of the `/etc/passwd` file is the password. These passwords are stored in an encrypted fashion by the operating system. If this field becomes damaged in any way, that user will not be able to log in to the system until the administrator assigns a new password to this account.

You can use this field to prevent a user from logging in to the system by placing an asterisk (**\****) in this field. Although the user will be unable to log in, she might still gain access remotely and run commands, so don't depend on this method as your only line of defense.

If you need to temporarily restrict a user's access, place an asterisk at the beginning of the password field for her account. Be careful not to make any other changes to this field. Although this is not 100 percent foolproof, it is usually adequate. You can use this method for users who are on vacation or away for an extended period of time. If this field is left empty, only the username is required to log in. The user will not be prompted for a password. Although this is sometimes helpful, if you want to have a guest account, it is also a significant security risk. Make sure that if you have an account with a blank password, you lock the account's access down as much as possible.

### User ID Field

The third field in each record is the user ID (UID). The system tracks users by UID rather than by name. For example, when a user starts a process, his UID is associated with that process and is displayed when using the ps command. Generally, ranges of UIDs are used to define the type of account. UIDs less than 100 are usually reserved for system accounts, root always has a UID of 0, and users are given UIDs greater than 100. The starting number for user IDs varies with different distributions but the principle is the same. The beginning user ID is defined in the `/etc/login.defs` file, an example of which might look like the following:

```
# *REQUIRED*
#	Directory where mailboxes reside, _or_ name of file, relative to the
#	home directory.  If you _do_ define both, MAIL_DIR takes precedence.
#	OMAIL_DIR is for Omail
#	OMAIL_DIR	Maildir
MAIL_DIR	/var/spool/mail
MAIL_FILE	.mail

# Password aging controls:
#	PASS_MAX_DAYS	Maximum number of days a password may be used.
#	PASS_MIN_DAYS	Minimum number of days allowed between password changes.
#	PASS_MIN_LEN	Minimum acceptable password length.
#	PASS_WARN_AGE	Number of days warning given before a password expires.

PASS_MAX_DAYS	99999
PASS_MIN_DAYS	0
PASS_MIN_LEN	5
PASS_WARN_AGE	7

UID_MIN                    500
UID_MAX                   60000

# Min/max values for automatic gid selection in groupadd
#
GID_MIN                    500
GID_MAX                   60000

# Require password before chfn/chsh can make any changes.
#
CHFN_AUTH                 yes

# Don't allow users to change their 'real name' using chfn.
#
CHFN_RESTRICT             yes

# If defined, this command is run when removing a user.
# the user to be removed (passed as the first argument).
#
#USERDEL_CMD      /usr/sbin/userdel_local

# If useradd should create home directories for users by default
# This option is ORed with the -m flag on useradd command line.
#
CREATE_HOME       yes
```

### Group ID Field

The group ID (GID) is used to define what group the user is a member of when she logs in. This is referred to as the user’s default login group. Groups are used to organize users. The GID is used by the operating system to track file permissions and is defined in the `/etc/group` file, which is discussed later in this chapter.

System groups are usually numbered 0–49, and the numbering of user groups starts at 50 or more depending on the distribution. The beginning user group ID is defined in the `/etc/login.defs` file.

On many systems, a default group called group or users gets the first GID available for use by a user group. All users are then made members of this group.

### Comments Field

This is not a required field but can be used to provide useful information. If the field is left blank, be sure to include the colon to designate that it is blank.

Most commonly, this field includes the user's full name, but it also can include phone numbers, departments, and other information. The `finger` command uses this field when returning user information. Email systems also can use this field to show who is sending mail.

### Home Directory Field

When a user logs on to the system, the login process uses this field to determine where to locate the user in the directory structure after a successful login. For users, this field usually contains the path to the user's home directory. If this field contains an invalid directory name, the user's login attempt will fail.

### Login Command Field

This field defines what command to execute when the login process terminates. Most of the time this will be a command that will start a shell program. This command can be used to restrict what a user can perform, such as to run a single application. If this field is left blank, the default shell is usually run.

This entry can be changed by the user by using the command `chsh`. The command `chsh` consults the `/etc/shells` file to determine whether the user's entry is valid.

### The passwd Command

Passwords are changed using the `passwd` command. Any user can change his own password, and root can change any user's password. The syntax for `passwd` is

```
passwd [user]
```

When a user changes his password, he does not need to specify his username; however, he will be prompted for his old password before entering the new one. When root changes a user's password, it specifies the username but does not have to know the user's present password.

The `passwd` command requires that the new password be entered twice before it is changed. This helps prevent users locking themselves out by making a typographical mistake.

![](img/8c0f494a2e9a2273fb49af52267f311e_179_0.png)

### Key Concept

The **passwd** command is used to change passwords. Users can change only their own passwords, but root can change anyone's password.

Many passwords also can be changed at once as a batch by using the **chpasswd** command by root. Its syntax is

```
chpasswd [option]
```

The **chpasswd** command reads a file containing the username and password combinations in the format *username:password* with one user's entry per line.

By default, the **chpasswd** command encrypts the password before storing it. However, you can provide the passwords in an encrypted format and use the `-e` option, which will prevent **chpasswd** from performing any encryption.

Password characteristics are defined in the `/etc/login.defs` file. Use this file to define how long a password must be, when the password expires, and how long before expiration the user will be prompted to change her password. It also defines the directory where mailboxes are.

Passwords are your first line of defense in protecting your system. You should periodically educate your users about the need to not share their passwords, to change their passwords on a regular basis, and to choose a good password.

Passwords should be at least six characters in length. Using a dictionary word, username, pet or spouse name, or other easily guessed password should be discouraged. The use of mixed case, numbers, and symbols strengthens your passwords. Because the strongest passwords are also those that are the hardest to remember, they are often written down and stored on the monitor, under the keyboard, or in a desk drawer.

One way to prevent this behavior is to encourage your users to use two easily remembered words joined by a symbol, such as dog$cat. This password can be further strengthened by either adding numbers and/or uppercase characters, such as 10og$Cat. If users construct their passwords in this manner, they create stronger passwords that they can remember easily.

![](img/8c0f494a2e9a2273fb49af52267f311e_179_1.png)
