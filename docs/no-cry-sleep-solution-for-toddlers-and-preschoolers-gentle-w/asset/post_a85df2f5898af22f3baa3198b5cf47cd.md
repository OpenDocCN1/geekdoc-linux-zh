
| Options | Description |
|---|---|
| -d dir | Sets the home directory of the new user. |
| -D | Displays defaults for all settings. Can also be used to reset default settings for the home directory (-b), group (-g), shell (-s), expiration date (-e), and password expirations (-f). |
| -e mm/dd/yy | Sets an expiration date for the account (none, by default). Specified as month/day/year. |
| -f days | Sets the number of days an account remains active after its password expires. |
| -g group | Sets a group. |
| -m | Creates user's home directory, if it does not exist. |
| -m -k skl-dir | Sets the skeleton directory that holds skeleton files, such as .profile files, which are copied to the user's home directory automatically when it is created; the default is /etc/skel. |
| -M | Does not create user's home directory. |
| -p password | Supplies an encrypted password (crypt or MD5). With no argument, the account is immediately disabled. |
| -r | A Red Hat-specific option that creates a system account (one whose user ID is lower than the minimum set in login.defs). No home directory is created unless specified by -m. |
| -s shell | Sets the login shell of the new user. This is /bin/bash by default, the BASH shell. |
| -u userid | Sets the user ID of the new user. The default is the increment of the highest number used so far. |
TABLE 28-3 Options for useradd and usermod

## usermod

The usermod command enables you to change the values for any of these features. You can change the home directory or the user ID. You can even change the username for the account. The usermod command takes the same options as useradd, listed in Table 28-3.

## userdel

When you want to remove a user from the system, you can use the userdel command to delete the user's login. With the -r option, the user's home directory will also be removed. In the next example, the user chris is removed from the system:

```
# userdel -r chris
```

## Managing Groups

You can manage groups using either shell commands or window utilities like the Red Hat User Manager.

## /etc/group and /etc/gshadow

The system file that holds group entries is called /etc/group. The file consists of group records, with one record per line and its fields separated by colons. A group record has four fields: a group name, a password, its ID, and the users who are part of this group. The Password field can be left blank. The fields for a group record are as follows:

- Group name The name of the group, which must be unique
- Password With shadow security implemented, this field is an x, with the password indicated in the /etc/gshadow file.
- Group ID The number assigned by the system to identify this group
- Users The list of users that belong to the group, separated by commas

Here is an example of an entry in an /etc/group file. The group is called engines, the password is managed by shadow security, the group ID is 100, and the users who are part of this group are chris, robert, valerie, and aleina.

```
engines:x:100:chris,robert,valerie,aleina
```

As in the case of the /etc/passwd file, it is best to change group entries using a group management utility like groupmod, groupadd, or the Red Hat User Manager. All users have read access to the /etc/group file. With shadow security, secure group data such as passwords are kept in the /etc/gshadow file, to which only the root user has access.

## User Private Groups

A new user can be assigned to a special group set up for just that user and given the user's name. Thus the new user dylan is given a default group also called dylan. The group dylan will also show up in the listing of groups. This method of assigning default user groups is called the User Private Group (UPG) scheme. UPG is currently used on Red Hat systems. The supplementary groups are additional groups that the user may want to belong to. Traditionally, users were all assigned to one group named users that would subject all users to the group permission controls for the users group. With UPG, each user has its own group, with its own group permissions.

## Group Directories

As with users, you can create a home directory for a group. To do so, you simply create a directory for the group in the /home directory and change its group to that of the group, along with allowing access by any member of the group. The following example creates a directory called engines and changes its group to that of the engines group:

```
mkdir /home/engines
chgrp engines /home/engines
```
