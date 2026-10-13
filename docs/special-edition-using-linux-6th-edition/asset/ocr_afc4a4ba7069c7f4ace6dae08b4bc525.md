# Browse Options

This option controls whether the printer share can be seen in the Network Neighborhood.

# Miscellaneous Options

The few options that are available here are the same as those that are found in the Shares section under Miscellaneous Options.

# Restricting Access to Services

The Samba server configuration is extremely flexible. It can make use of UNIX NIS groups for access control, giving certain users read-only access, others read-write access, some users admin access, and still others no access. It can also force all users to be treated as members of the guest account (which is, by default, the UNIX user nobody) or as another special user. It can force users to belong to a certain group. All these options and more are part of the Shares page, in the Security Options section under Advanced View. Specifically, these options are Valid and Invalid Users, Admin Users, Read List, Write List (which is both Read and Write), Force User, and Force Group.

By making use of these advanced options, very tight control can be maintained over users’ connections to any given share. An option is also on the Global page to set a root directory to something other than the default of /.

> **Caution**
> 
> If you set the root directory, make sure that everything that is required to run the Samba server, plus binaries and all the libraries that are used by users, is copied below this new root directory. This functions the same as the FTP chroot command.

# Variables Available to Samba

If you’ve followed along in swat and looked at any of the default entries on the Advanced View pages, you’ve seen variables in the form %X, where X is one of many upper- or lower-case letters. These variables can be used to extend the flexibility of Samba. Following is a list of the variables and a short explanation of each:

+   - `%S`—The name of the current service, if any.
+   - `%P`—The root directory of the current service, if any.
+   - `%u`—Username of the current service, if any.
+   - `%g`—Primary group name of `%u`.
+   - `%U`—Session username (the username that the client requested, not necessarily the same as the one received).
+   - `%G`—Primary group name of `%U`.
+   - `%H`—The home directory of the user (`%u`).