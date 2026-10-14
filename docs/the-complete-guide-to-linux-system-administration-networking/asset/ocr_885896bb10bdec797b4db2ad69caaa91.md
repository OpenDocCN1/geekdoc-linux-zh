# CHAPTER SUMMARY

+   - User accounts can be managed graphically using system-config-users, Webmin, YAST, or similar tools in various Linux distributions. User accounts can also be managed very effectively from the command line.
+   - When changing UIDs or GIDs, you must be careful not to leave files that have the old UID or GID assigned. When deleting user or group accounts, you must be careful not to reuse a user or group name inadvertently.
+   - The `useradd` command is used to create user accounts on the command line. It relies on default settings that you can view with the `-D` option. The `groupadd` command is used to create new groups.
+   - The `usermod` command is used to modify existing user accounts. The `groupmod` command is used to modify existing group accounts.
+   - Password expiration details can be configured using the `chage` command, or using most graphical user configuration tools.
+   - When new user accounts are created, the contents of the `/etc/skel` directory is copied into the new home directory of the user. The `/etc/login.defs` file also defines some default information for new user accounts.
+   - User accounts can be disabled using the `passwd` command or deleted using the `userdel` command. Some system administrators prefer to never delete a user account, but only disable them and remove the user's files.
+   - The SUID and SGID permissions cause a user to assume the permissions of the owner of an executable file when that program is executed. These special permissions are useful but can be very dangerous if used on untrusted program files.
+   - The sticky bit and several other special file permission arrangements permit a system administrator to carefully control how multiple users can work with files in shared directories.
+   - To set the sticky bit, SUID, or SGID, you can use `chmod` with either an additional digit (in the numeric mode) or an `s` or `t` (in letter mode).
+   - System administrators can communicate with users using `wall`, using the `/etc/motd` file, or via e-mail, selecting whichever method is most appropriate for the message to be delivered.
+   - The `sudo` program lets regular users perform tasks that require root privileges. The program is configured using the `/etc/sudoers` file, which you must edit using the `visudo` command.
+   - Each line in `/etc/sudoers` configures a user or group with permission to use certain commands on a certain computer system. Sample configurations make a basic setup easy to configure, but errors in `sudo` configuration can lead to serious security breaches.