
# 148 Linux Administration: A Beginner's Guide

This command will create a new user account called yyang. The user will be created with the usual Fedora default attributes. The entry in the /etc/passwd file will be

`yang:x:1001:1001:Yyang Yang:/home/yyang:/bin/bash`

From this entry, you can tell these things about the Fedora (and RHEL) default user values:

- The UID is the same as the GID number. The value is 1001 in this example.
- The default shell for new users is the Bash shell (/bin/bash).
- A home directory is automatically created for all new users (for example, /home/yyang).

- 2. Use the password command to create a new password for the username yyang. Set the password to 1gan19, and repeat the same password when prompted. Type the following:

```bash
[root@server]# password yyang
Changing password for user yyang
...<OUTPUT TRUNCATED>...
```

> NOTE Several PAM modules may be called whenever the password command is called. For example, on Red Hat-like systems, one of the modules is responsible for checking that the selected password meets the password strength policies on the system—policies such as the password length, complexity, and so on. The module called in the previous example is pam_pwquality.so. To learn more about this particular module, see its manual page pam_pwquality.

- 3. Create another user account called mellow for the user, with a full name of "Mel M", but this time, change the default Fedora behavior of creating a group with the same name as the user. (This is caused by the -n option and this user will intend to belong to the general user groups.) Type this:

```bash
[root@server]# usermadd -c "Mel Mellow" mellow
```

- 4. Use the id command to examine the properties of the user mellow:

```bash
[root@server]# id mellow
```

- 5. Again, use the password command to create a new password for the account mellow. Set the password to 2owl!7, and repeat the same password when prompted:

```bash
[root@server]# password mellow
```

# CHAPTER 5 Managing Users and Groups

6. Create the final user account, called bogus. But this time, specify the user’s shell to be the tcsh shell, and let the user’s default primary group be the system “games” group:

```bash
[root@server ~]# useradd -s /bin/tcsh -g games bogus
```

7. Examine the /etc/passwd file for the entry for the bogususer:

```bash
[root@server~]# grep bogususer /etc/passwd
bogususer:x:1003:/home/bogususer:/bin/tcsh
```

From this, you can tell the following:

- The UID is 1003.
- The GID is 20.
- A home directory is also created for the user under the /home directory.
- The user’s shell is /bin/tcsh.

## Creating Groups with groupadd

Next, create a couple of groups, nonsystem and system.

- 1. Create a new group called research:

```bash
[root@server ~]# groupadd research
```

- 2. Examine the entry for the research group in the /etc/group file:

```bash
[root@server ~]# grep research /etc/group
research:x:1002:
```

This output shows that the group ID for the research group is 1002.

- 3. Create another group called sales:

```bash
[root@server ~]# groupadd sales
```

- 4. Create the final group called bogus, and force this group to be a system group (that is, the GID will be lower than 999). Type the following:

```bash
[root@server ~]# groupadd -r bogus
```

- 5. Examine the entry for the bogus group in the /etc/group file:

```bash
[root@server ~]# grep bogus /etc/group
bogus:x:988:
```

The output shows that the group ID for the bogus group is 988.

## Modifying User Attributes with usermod

Now using usermod to change the user and group IDs for a couple of accounts.

- 1. Use the usermod command to change the user ID (UID) of the bogususer to 1600:

```bash
[root@server ~]# usermod -u 1600 bogususer
```

- 2. Use the id command to view your changes:

```bash
[root@server ~]# id bogususer
uid=1600 (bogususer) gid=20 (games) groups=20 (games)
```

The output shows the new UID (1600) for the user.

- 3. Use the usermod command to change the primary GID of the bogususer to that of the bogus group (GID = 988) and also to set an expiry date of 12-12-2019 for the account:

```bash
[root@server ~]# usermod -e 2019-12-12 bogususer
```

- 4. View your changes with the id command:

```bash
[root@server ~]# id bogususer
uid=1600 (bogususer) gid=20 (games) groups=20 (games)
```

- 5. Use the change command to view the account information:

```bash
[root@server ~]# change bogususer
Last password change               : Oct 26, 2019
Password expires                     : never
Password inactive                  : never
Minimum days of password change : 0
Maximum days between password change : 999
Number of days before expires         : 7

NOTE Several PAM modules may be called whenever the password command is called. For example, on Red Hat-like systems, one of the modules is responsible for checking that the selected password meets the password strength policies on the system—policies such as the password length, complexity, and so on. The module called in the previous example is pam_pwquality.so. To learn more about this particular module, see its manual page pam_pwquality.

Next, create a couple of groups, nonsystem and system.

- 1. Create a new group called research:

```bash
[root@server ~]# groupadd research
```

- 2. Examine the entry for the research group in the /etc/group file:

```bash
[root@server ~]# grep research /etc/group
research:x:1002:
```

This output shows that the group ID for the research group is 1002.

- 3. Create another group called sales:

```bash
[root@server ~]# groupadd sales
```

- 4. Create the final group called bogus, and force this group to be a system group (that is, the GID will be lower than 999). Type the following:

```bash
[root@server ~]# groupadd -r bogus
```

- 5. Examine the entry for the bogus group in the /etc/group file:

```bash
[root@server ~]# grep bogus /etc/group
bogus:x:988:
```

The output shows that the group ID for the bogus group is 988.

- 1. Use the usermod command to change the user ID (UID) of the bogususer to 1600:

```bash
[root@server ~]# usermod -u 1600 bogususer
```

- 2. Use the id command to view your changes:

```bash
[root@server ~]# id bogususer
uid=1600 (bogususer) gid=20 (games) groups=20 (games)
```

The output shows the new UID (1600) for the user.

- 3. Use the usermod command to change the primary GID of the bogususer to that of the bogus group (GID = 988) and also to set an expiry date of 12-12-2019 for the account:

```bash
[root@server ~]# usermod -e 2019-12-12 bogususer
```

- 4. View your changes with the id command:

```bash
[root@server ~]# id bogususer
uid=1600 (bogususer) gid=20 (games) groups=20 (games)
```

- 5. Use the change command to view the account information:

```bash
[root@server ~]# change bogususer
Last password change               : Oct 26, 2019
Password expires                     : never
Password inactive                  : never
Minimum days of password change : 0
Maximum days between password change : 999
Number of days before expires         : 7
