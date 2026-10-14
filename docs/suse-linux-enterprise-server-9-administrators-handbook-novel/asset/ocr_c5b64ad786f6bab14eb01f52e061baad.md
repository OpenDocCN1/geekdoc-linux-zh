# LISTING 4.2
User and Group-Related Directives in /etc/login.defs (continued)

```
#
# Min/max values for automatic gid selection in groupadd
#
# SYSTEM_GID_MIN to SYSTEM_GID_MAX inclusive is the range for
# GIDs for dynamically allocated administrative and system
# groups.
# GID_MIN to GID_MAX inclusive is the range of GIDs of
# dynamically allocated groups.
SYSTEM_GID_MIN        100
SYSTEM_GID_MAX        499
GID_MIN               1000
GID_MAX               60000

#
# User/group names must match the following regex expression.
# The default is [A-Za-z_][A-Za-z0-9_.$-]*[A-Za-z0-9_.$-]\?
#
CHARACTER_CLASS      [A-Za-z_][A-Za-z0-9_.$-]*[A-Za-z0-9_.$-]\?

#
# Umask which is used by useradd and newusers for creating
# new home directories.
UMASK                 022

#
# If defined, this command is run when adding a user.
# It should rebuild any NIS database etc. to add the
# new created account.
#
USERADD_CMD           /usr/sbin/useradd.local

#
# If defined, this command is run before removing a user.
# It should remove any at/cron/print jobs etc. owned by
# the user to be removed.
#
USERDEL_PRECMD        /usr/sbin/userdel-pre.local

#
# If defined, this command is run after removing a user.
# It should rebuild any NIS database etc. to remove the
# account from removed.
#
USERDEL_POSTCMD       /usr/sbin/userdel-post.local
```