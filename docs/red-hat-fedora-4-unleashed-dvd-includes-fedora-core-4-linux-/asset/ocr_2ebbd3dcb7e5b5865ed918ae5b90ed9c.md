This command confines the user to a specific directory structure in the same way anonymous users are confined to /var/ftp. This command also limits these users to access files for which their assigned group has permissions.

The groupname parameter can be the name of a group or that group's corresponding GID (Group ID). If you use a GID as the groupname parameter, put a percentage symbol (%) in front of it. You can use this command to assign permissions to a range of group IDs, as in this example:

```
guestgroup %500-550
```

This entry would restrict all users with the group IDs 500–550 to be treated as a guest group, rather than individual users. In order for guestgroup to work, you must set up the user's home directories with the correct permissions, exactly like the anonymous FTP user.

# Limit Permissions Based on Individual ID

The guestuser line works exactly like the guestgroup command you just read about, except it specifies a User ID (UID) instead of a group ID. Here's the command:

```
guestuser <username> [<username>]
```

This command limits the guest user to files for which the user has privileges. Generally, a user has more privileges than a group, so this type of assignment can be less restrictive than the guestgroup line.

# Restrict the Number of Users in a Class

limit restricts the number of users in a class during given times. Here is the command, which contains fields for specifying a class, a number of users, a time range, and the name of a text file that contains an appropriate message:

```
limit <class> <n> <times> <message_file>
```

If the specified number of users from the listed class is exceeded during the given time period, the user sees the contents of the file given in the message_file parameter.

The times parameter is somewhat terse. The format for this is a comma-delimited string in the form of days, hours. Valid day strings are Su, Mo, Tu, We, Th, Fr, Sa, and Any. The hours are formatted in a 24-hour format. An example is as follows:

```
limit anonymous 10 MoTuWeThFr,Sa0000-2300 /home/ftp/.message_limit_anon_class
```

This line will limit the anonymous class to 10 concurrent connections on Monday through Friday, and on Saturday from midnight to 11:00 p.m. If the number of concurrent connections is exceeded or at 11:00 p.m. on Saturday, the users will see the contents of the file /home/ftp/.message_limit_anon_class.

Syntax for finer control over limiting user connections can be found in the ftpaccess man page.