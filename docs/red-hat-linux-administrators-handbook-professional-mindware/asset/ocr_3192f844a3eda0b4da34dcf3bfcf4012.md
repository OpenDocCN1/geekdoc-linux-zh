# Listing 5-3 Continued

```
# It should remove any at/cron/print jobs etc. Owned by
# the user to be removed (passed as the first argument).
#
#USERDEL_CMD /usr/sbin/userdel_local

#
# If useradd should create home directories for
# users by default on RH systems, we do. This option is
# ORed with the -m flag on useradd command line.
#
CREATE_HOME yes
```

Because the comments in this file are sufficient to explain the configuration details, they are not discussed any further here.

# Managing Users with linuxconf

The linuxconf command can be used to perform all the user administration tasks. This section uses the X Window–based interface for linuxconf.

# Adding a new user account

To access the user administrative interface in linuxconf, select the Config→ Users accounts→ Normal → User accounts option.
To add a new user, follow these steps:

+   1. Click the Add button on the right side of the window. A new window with multiple tabs appears.
+   2. In the Base Info tab, enter the Login name (username), Full name, group, Supplementary groups (optional), Home directory (optional), Command interpreter (optional), and User ID (optional). You can also choose to create this account but not yet enable it, by deselecting the This account is enabled check box.