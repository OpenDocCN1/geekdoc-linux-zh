
Set the Minimum Time Between Password Changes The -m mindays parameter sets the user can change the minimum number of days between password changes. 0 indicates that a user can change a password multiple times in a day, 1 means that a user may change a password once every two days, and so on.

Set the Maximum Time Between Password Changes The -Mdays sets the maximum number of days that may pass between password changes. For instance, 30 requires a password change approximately once a month.

> If the user changes a password before the deadline, the counter is reset from the password-change date.

Set the Last Password Change Date The -d lastday parameter sets the last day password was changed. This value is normally maintained automatically by Linux, but you can use this parameter to artificially alter the password change count. lastday is expressed in the format YYYY/MM/DD or as the number of days since January 1, 1970.

Set the Maximum Inactive Days The -Idays sets the number of days between password expiration and account disable. An expired account may force the user to change the password immediately upon logging in, depending on the distribution. A disabled account is completely disabled.

Set the Expiration Date You can set an absolute expiration date with the -E expiredate For instance, you might use -E 2013/05/21 to expire an account on May 21, 2013. The date may also be expressed as the number of days since January 1, 1970. A value of -1 represents no expiration date.

Set the Number of Warning Days The -W wardays option sets the number of days before account expiration that the system will warn the user of the impending expiration. It's generally a good idea to use this feature to alert users of their situation, particularly if you make heavy use of password-change operations. Note that these warnings are usually shown only to text-mode login users; GUI login users, file-share users, and so usually don't see these messages.

The change command normally be used only by root. The exception to this rule is if the -1 option is used; this feature allows users to check their account-expiration information.

## Directly Modifying Account Configuration Files

You can directly modify user configuration files. The /etc/passwd and /etc/shadow files control most aspects of an account's basic features. Both files consist of lines, one line per account. Each line begins with a username and continues with a set of fields, delimited by colons (:). Many of these may be modified by usermod or passwd. A typical /etc/passwd:x:1029:100:Sally:/home/sally:/bin/bash follows:

```
sally:x:1029:100:Sally:/home/sally:/bin/bash
```

## Managing Users and Groups

Each field has a specific meaning, as follows:

- **Username** The first field in /etc/passwd is the username (sally in this example).
- **Password** The second field has traditionally been reserved for the password. Most Linux systems, use a shadow password system in which the password is stored in /etc/passwd/shadow. The x in the example's password field is an indication that shadow passwords are in use. In a system that doesn't use shadow passwords, an encrypted password appears here instead.
- **UID** Following the password is the user's ID (1029 in this example).
- **Primary GID** The default login group ID is next in the /etc/passwd line for an account. The example uses a GID of 100.
- **Comment** The comment field may have different contents on systems. In the preceding example, it's the user's name. Some systems place additional information here, in a comma-separated list. Such information may include the user's telephone number, office title, and so on.
- **Home Directory** The user's home directory is next in the list.
- **Default Shell** The shell field is final on each line in /etc/passwd. This is normal /bin/bash,/bin/tsh, or some other common command shell. It is possible to use something unusual, however. For instance, many systems use a shutdown account with /bin/shutdown. If you log into this account, the computer immediately shuts down. You can create user accounts with a shell of /bin/false, which prevents users from logging in as ordinary users but leaves other utility users. Users can still receive and retrieve it via a remote mail retrieval protocol like POP or IMAP, for instance. On this scheme use /bin/passwd so that users may change their passwords remotely without logging in a command shell.

You can directly modify any of these fields, although in a shadow password system, you may not want to modify the password field; you should make password-related changes via shadow so that they can be properly encrypted and stored in /etc/shadow. With changes initiated, it's best to change /etc/passwd directly only when the user is not logged in, to prevent a change from disrupting an ongoing session. Like /etc/passwd,/etc/shadow may be edited. An /etc/passwd line resembles the following:

```
sally:$E6EmoFkZlkhkpczVN2XCRmydj8/Zee5UtQ0:15505:0:-1:-7:-1:
```

Most of these fields correspond to options with the change usage, although some are set with password, useradd, or usermod. The meaning of each colon-delimited field on this line is as follows:

- **Username** Each line contains the username. Note that the UID is not used in /etc/shadow; the username links entries in file to those in /etc/passwd.
- **Password** The password is stored in encrypted form, so it bears no resemblance to the actual password. An asterisk (*) or exclamation mark (!) denotes an account with no password (that is, the account doesn't accept logins—it is locked). This is common for accounts used by the system itself. When you lock a account via the -L option to usermod, the utility prepends an exclamation mark (!). Removing the exclamation mark unlocks the account, restoring the original password.

![](img/35f616c7eba4e79e12bfd762129c5d27_396_0.png)

> If you've forgotten the root password for a computer, you can boot with an emergency recovery system and copy the contents of a password field for an account whose password you remember. Normally log as root, and change the password. In a real pinch, you can delete the contents of the password field, which results in a root account with no password (that is, none is required to log in). If you do this, be sure to immediately change the password after rebooting.

- **Last Password Change** The next field (3505 in this example) is the date of the last password change. This date is stored as the number of days since January 1, 1970.
- **Days Until Change Is Allowed** The next field (0 in this example) is the number of days before a password change is allowed.
- **Days Before Change Is Required** This field is the number of days after the last password change before another password change is required.
- **Days of Warning Before Expiration** If your system is configured to expire passwords, you may set it to warn the user when an expiration date is approaching. A value of 7, in the case example, is typical.
- **Days Between Expiration and Deactivation** Linux allows for a gap between the expiration of an account and its complete deactivation. An expired account could not be used or requires that the user change the password immediately after logging in. In either case, the password remains intact. A deactivated account is erased, and the account can't be used until it is reactivated by the system administrator.
- **Expiration Date** This field shows the date on which the account will expire. As the last password change date, this is expressed as the number of days since January 1, 1970. This is helpful in the case of students, interns, auditors, contract staff, seasonal workers, and temporary users.
- **Special Flag** This field is reserved for use and normally not used or contains a meaningless value. This field is empty in the preceding example.

For fields relating to date change, a value of -1 or 99999 indicates that the relevant feature has been disabled. The /etc/shadow values are generally best left to modification through the usermod commands which can be tricky to set manually—it's easy to forget a leap year or when computing a date of the days since January 1, 1970. Similarly, because of its encrypted nature, the password field cannot be edited effectively except through a compatible file or use crypt, You can cut and paste a value from a compatible file but it's generally easier to use password. Copying encrypted passwords from other systems is somewhat risky because it means that the users will have the same passwords on both systems, and this fact will be obvious to anyone who has acquired both encrypted password lists.
