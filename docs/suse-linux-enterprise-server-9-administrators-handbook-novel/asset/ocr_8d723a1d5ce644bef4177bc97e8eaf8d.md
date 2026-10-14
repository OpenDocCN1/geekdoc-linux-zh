# CAUTION

It's best not to change the `SYSTEM_UID_*` and `SYSTEM_GID_*` directive settings as that may cause some application not to function properly.

The `UMASK` directive in `/etc/login.defs` is used by useradd and YaST to set the proper file permissions on the home directory. Refer to Chapter 6 for information about file ownership and permissions. The `USERDEL_PRECMD` and `USERDEL_POSTCMD` directives point to two templates that you can customize for your particular needs. For instance, you may want to copy the user's home directory elsewhere before you delete the user ID. The default script for the `USERDEL_PRECMD` directive deletes any cron jobs belonging to the user, whereas the default `USERDEL_POSTCMD` does nothing.

# TIP

Settings in `/etc/login.defs` can be edited using YaST from the YaST Control Center, select Security and Users, Security Settings. If the Current Security Setting is one of Level 1 through Level 3, click Details. If the selection is Custom Settings, click Next. You are then presented with a series of screens, each dealing with a different set of directives found in `/etc/login.defs`.

Where redundancy exists between `/etc/login.defs` and `/etc/default/useradd`, the settings in `/etc/login.defs` take precedence.

# Creating and Editing Groups

The process for managing groups is similar to that for users. Rather than listing many of the same steps again, we’ve listed the salient differences here instead:

+   - From the YaST Control Center, select Security and Users, Edit and Create Groups to launch the User and Group Administration module. If you are already in the User and Group Administration module, click on the Groups radio button near the top of the screen; you can use the Users and Groups radio buttons to switch back and forth between managing users and groups.
+   - When launching YaST from a terminal session, you can use `yast groups` or `yast2 groups` to skip over the YaST Control Center and go directly to the User and Group Administration module.
+   - Shown in Figure 4.3 is the screen for adding a new local group. You need to provide a group name and optionally select one or more users who will be members of this group.