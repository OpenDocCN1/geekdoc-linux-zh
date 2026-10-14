```
# Log successful and failed sudo attempts to the file
/var/log/sudo
local2.debug                                      /var/log/sudo
# All the logs which goes to /var/su/log are also sent to a remote machine.
# where "loghost" is the name of the remote machine.
local2.debug                                      @loghost
```

The --with-mailto option is also strongly recommended so that each time a user attempts to access a command for which they don't have the proper authority, an email is sent to alert the system administrator. To configure the user functionality of sudo, you'll need to edit the file called sudoers. Note that this file needs to be edited by using the visudo program which comes with the sudo package, as using less secure, standard editing programs may introduce problems that could be used to exploit sudo. A simple example of the sudoers file is:

```
##
# Host alias specification
##
Host_Alias LABHOSTS = host1, host2, host3

##
# User alias specification
##
User_Alias LABUSERS = user1, user2

##
# Cmd alias specification
##
Cmd_Alias CLEARQUEUE = /usr/ucb/lprm
LABUSERS LABHOSTS = CLEARQUEUE
```

In this case, user1 and user2 are granted the right to clear the printing queue on host1, host2, and host3.

Under Windows 2000, by using the Security Configuration Toolset, it is possible to grant some limited administrative privileges to regular users such as:

+   - Increasing quotas.
+   - Performing backups and restores.
+   - Initiating the shutdown of remote systems.

For printers, two privilege rights can be given to users by editing the properties of the printer:

+   - Manage printers.
+   - Manage documents.