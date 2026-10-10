
## Password
The second field has traditionally been reserved for the password. Most Linux systems, however, use a shadow password system in which the password is stored in /etc/shadow. The x in the example’s password field is an indication that shadow passwords are in use. In a system that doesn’t use shadow passwords, an encrypted password appears here instead.

## UID
Following the password is the account’s user ID (529 in this example).

## Primary GID
The default login group ID is next in the /etc/passwd line for an account. The example uses a primary GID of 100.

## Comment
The comment field may have different contents on different systems. In the preceding example, it’s the user’s full name. Some systems place additional information here, in a comma-separated list. Such information may include the user’s telephone number, office number, title, and so on.

## Home directory
The user’s home directory is next up in the list.

## Default shell
The default shell is the final item on each line in /etc/passwd. This is normally /bin/bash, /bin/tcsh, or some other common command shell. It’s possible to use something unusual here, though. For instance, many systems include a shutdown account with /bin/shutdown as the shell. If you log into this account, the computer immediately shuts down. You can create user accounts with a shell of /bin/false, which prevents users from logging in as ordinary users but leaves other utilities intact. Users can still receive mail and retrieve it via a remote mail retrieval protocol like POP or IMAP, for instance. A variant on this scheme uses /bin/passwd so that users may change their passwords remotely but can’t log in using a command shell.

You can directly modify any of these fields, although in a shadow password system, you probably do not want to modify the password field; you should make password-related changes via passwd so that they can be properly encrypted and stored in /etc/shadow. As with changes initiated via usermod, it’s best to change /etc/passwd directly only when the user in question isn’t logged in, to prevent a change from disrupting an ongoing session.

Like /etc/passwd, /etc/shadow may be edited directly. An /etc/shadow line resembles the following:

```
sally:E/moFkeTU5nTq:14069:0:-1:7:-1:-1:
```

Most of these fields correspond to options set with the chage utility, although some are set with passwd, useradd, or usermod. The meaning of each colon-delimited field on this line is as follows:

### Username
Each line begins with the username. Note that the UID is not used in /etc/shadow; the username links entries in this file to those in /etc/passwd.

### Password
The password is stored in encrypted form, so it bears no obvious resemblance to the actual password. An asterisk (*) or exclamation mark (!) denotes an account with no password (that is, the account doesn’t accept logins—it’s locked). This is common for accounts used by the system itself.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_401_0.png)

If you've forgotten the root password for a system, you can boot with an emergency recovery system and copy the contents of a password field for an account whose password you do remember. You can then boot normally, log in as root, and change the password. In a real pinch, you can delete the contents of the password field, which results in a root account with no password (that is, none is required to log in). If you do this, be sure to immediately change the root password after rebooting!

### Last password change
The next field (14069 in this example) is the date of the last password change. This date is stored as the number of days since January 1, 1970.

### Days until a change is allowed
The next field (0 in this example) is the number of days before a password change is allowed.

### Days before a change is required
This field is the number of days after the last password change before another password change is required.

### Days of warning before password expiration
If your system is configured to expire passwords, you may set it to warn the user when an expiration date is approaching. A value of 7, as in the preceding example, is typical.

### Days between expiration and deactivation
Linux allows for a gap between the expiration of an account and its complete deactivation. An expired account either can't be used or requires that the user change the password immediately after logging in. In either case, its password remains intact. A deactivated account's password is erased, and the account can't be used until it's reactivated by the system administrator.

### Expiration date
This field shows the date on which the account will expire. As with the last password change date, the date is expressed as the number of days since January 1, 1970.

### Special flag
This field is reserved for future use and normally isn't used or contains a meaningless value. This field is empty in the preceding example.

For fields relating to day counts, a value of -1 or 99999 typically indicates that the relevant feature has been disabled. The /etc/shadow values are generally best left to modification through the usermod and chage commands because they can be tricky to set manually—for instance, it's easy to forget a leap year or the like when computing a date as the number of days since January 1, 1970. Similarly, because of its encrypted nature, the password field can't be edited effectively except through passwd or similar utilities. You can cut and paste a value from a compatible file or use crypt, but it's generally easier to use passwd. Copying encrypted passwords from other systems is also somewhat risky because it means that the users will have the same passwords on both systems, and this fact will be obvious to anybody who's acquired both encrypted password lists.

## Managing Users and Groups

The /etc/shadow file is normally stored with very restrictive permissions, such as rw------- (600), with ownership by root. (Precise permissions vary from one distribution to another, though.) This fact is critical to the shadow password system’s utility because it keeps non-root users from reading the file and obtaining the password list, even in an encrypted form. By contrast, /etc/passwd must be readable by ordinary users and usually has rw-r--r-- (644) permissions. If you manually modify /etc/shadow, be sure it has the correct permissions when you’re done.

## Real World Scenario

## Network Account Databases

Many networks employ network account databases. Such systems include the Network Information System (NIS), an update to this system called NIS+, the Lightweight Directory Access Protocol (LDAP), Kerberos realms, Windows NT 4.0 domains, and Active Directory (AD) domains. All of these systems move account database management onto a single centralized computer (often with one or more backup systems). The advantage of this approach to account maintenance is that users and administrators need not deal with maintaining accounts independently on multiple computers. A single account database can handle accounts on dozens (or even hundreds or thousands) of different computers, greatly simplifying day-to-day administrative tasks and simplifying users’ lives. Using such a system, though, means that most user accounts won’t appear in /etc/passwd and /etc/shadow, and groups may not appear in /etc/group. (These files will still hold information on local system accounts and groups, though.)

Linux can participate in these systems. In fact, some distributions provide options to enable such support at OS installation time. Typically, you must know the name or IP address of the server that hosts the network account database, and you must know what protocol that system uses. You may also need a password or some other protocol-specific information, and the server may need to be configured to accept accesses from the Linux system you’re configuring.

Activating use of such network account databases after installing Linux is a complex topic. It involves installing appropriate software, modifying the /etc/nsswitch.conf file, and modifying the Pluggable Authentication Module (PAM) configuration files in /etc/pam.d. Such systems often alter the behavior of tools such as passwd and usermod in subtle or not-so-subtle ways. If you need to use such a system, you’ll have to consult documentation specific to the service you intend to use. My book Linux in a Windows World (O’Reilly, 2005) covers this topic for Windows NT 4.0 domains, LDAP, and Kerberos; and Mark Minasi and Dan York’s Linux for Windows Administrators (Sybex, 2002) covers this topic for Windows NT 4.0 domains and NIS.
