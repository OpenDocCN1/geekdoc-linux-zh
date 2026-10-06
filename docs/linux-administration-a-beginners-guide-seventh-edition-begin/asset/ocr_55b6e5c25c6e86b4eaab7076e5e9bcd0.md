# 134 Linux Administration: A Beginner's Guide

Every option you specify when using this command results in that particular parameter being modified for the user. But all one of the parameters listed here are identical to the parameters documented for the useradd command. The one exception is -l

The -l option allows you to change the user's login name. The -u option are the only options that require special care. Before changing the user's login or UID, you must make sure the user is not logged into the system or running any processes. Changing this information if the user is logged in or running processes will cause unpredictable results.

# userdel

The userdel command does the exact opposite of useradd—it removes existing users. This straightforward command has only two commonly used parameters and one required parameter:

```
Usage: userdel [options] LOGIN
Options:
-f, --force    force removal of files, even if not owned by user
-r, --remove    remove home directory and mail spool
```

# groupadd

The group-related commands are similar to the user commands; however, instead of working on individual users, they work on groups listed in the /etc/group file. Note that changing group information does not cause user information to be automatically changed. For example, if you remove a group whose GID is 100 and a user's default group is 100, their default group will not be updated to reflect that the group no longer exists.

The groupadd command adds groups to the /etc/group file. The command-line options for this program are as follows:

```
Usage: groupadd [options] GROUP
```

Table 5-2 describes some common groupadd command options.

# groupdel

Even more straightforward than userdel, the groupdel command removes existing groups specified in the /etc/group file. The only usage information needed for this command is

```
Usage: groupdel group group
```

where group is the name of the group to remove.

# groupmod

The groupmod command allows you to modify the parameters of an existing group. The syntax and options for this command are shown here: