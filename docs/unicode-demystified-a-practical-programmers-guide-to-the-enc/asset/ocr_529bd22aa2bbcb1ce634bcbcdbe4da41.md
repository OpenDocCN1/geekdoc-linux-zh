root (or uses another method; see the list starting on page 898) in order to have systemwide powers that are beyond those of ordinary users: A user with root privileges is referred to as Superuser. The login name is root by default and should not be changed. Although you can set up a GNU/Linux system with any name in place of root, it will break the system: Many programs depend on this being root. Superuser has the following commands, and more:

+   - Some commands, as those that add users, partition hard drives, and change system configuration, can be executed only by root.

+   - Read, write, and execute file access and directory permissions do not affect root: Superuser can read from, write to, and execute all files, as well as examine and work in all directories.

+   - Some restrictions and safeguards are built into some commands do not apply to root. For example, root can change any user's password without knowing the old password.

When you are running with root (Superuser) privileges, the shell by convention displays a special prompt to remind you of your status. By default this prompt is or ends with a pound sign (#).

To lessen the chance that other than Superuser will try to use them by mistake, many of the commands that Superuser runs are kept in /sbin and /usr/sbin directories, rather than in /bin and /usr/bin. (Many of these commands can be run by ordinary users.) You can execute these commands by giving their full pathname on the command line (for example, /sbin/runlevel). When you log in as root, these directories are in your PATH by default.

# Least Privilege

When you are working on the computer, especially when you are working as the system administrator, perform any task using the least privilege possible. When you can perform a task logged in as an ordinary user, do so. When you must be logged in as Superuser, do as much as you can as an ordinary user, log in or su so that you have root privileges, do much of the task has to be done as Superuser, and revert to being an ordinary user as soon as you can. Because you are more likely to make a mistake when you are rushing, this concept becomes more important when you have less time to apply it.

2. Superuser can use certain tools, such as sudo, which is covered shortly, to give specific users permission to perform tasks that are normally reserved for Superuser.