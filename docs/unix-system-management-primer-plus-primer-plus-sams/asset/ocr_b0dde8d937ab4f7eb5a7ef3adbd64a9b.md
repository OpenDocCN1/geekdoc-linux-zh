# UNIX SYSTEM MANAGEMENT PRIMER PLUS

For example, a backup operator can su to a backup role and be allowed to run fsdump as root to back up a file system. Although this example works a like sudo, RBAC support is also built into certain commands, so you can assign specific authorizations to roles, not just certain commands. For instance, you can assign the solaris.jobs.admin authorization to a role, and that role would be able to read and edit anyone's crontab on the system using the crontab command. RBAC integration like this is limited; currently, only the following Solaris applications and commands have built-in RBAC support:

+   - Solaris Management Console
- at
- atq
- batch
- crontab
- allocate
- deallocate
- list_devices

Until more commands have integrated RBAC support that normally require root privileges, such as shutdown, reboot, useradd, and passwd, RBAC offers little more than the convenience of a built-in sudo.

# Using Unix Group Permissions to Edit Files

Ironically, most tasks that users believe they have root access to perform roles can actually be performed with some clever manipulation of group permissions. Processes that require root privileges need the privileges to read or edit root-owned files. However, if files are not critical to system stability, you can assign a new group to the file and enable group read and write permissions. This group permission allows root as well as the people in that group to read and write to the file.

A good example of where group permissions are useful is the Apache Web server's main configuration file, httpd.conf. The default permissions on this configuration look like this on Hat Linux:

```
-rw-r--r-- 1 root root 33998 Jul 17 2001 httpd.conf
```

The file is readable by everyone, but writable only by root. This setup requires you to give your Webmaster root privileges, possibly through sudo, to edit the file. Unless your Webmaster is the system administrator, who probably don't want to give him or her root privileges. You could change the ownership to the Webmaster or create a new account for him or her to su, but these methods are neither flexible nor efficient.

The most reasonable solution is to create a Unix group that is allowed to edit Web server configurations; you can then change the group and permissions on the file so that anyone in the web group can write to it, as follows: