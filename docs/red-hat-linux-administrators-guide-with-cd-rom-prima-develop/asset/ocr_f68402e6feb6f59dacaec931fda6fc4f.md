identifies each user’s home directory. This is the default location or directory that the user is sent to after logging on the system. It is here that the user keeps and edits startup files particular to his or her needs. The last field defines the user’s shell. See Chapter 6 for more information about customizing the separate fields found in the /etc/passwd file.

Linux also has users on the system who do not generally log in and do not require a shell. These are users who perform system tasks, but who do not exist as valid users with login capability. Examples of such users are nobody and xfs. The system requires a user account under which certain processes run, such as the web daemon or the X font server. The aforementioned “nonexistent” users run these two processes respectively. In such cases, the default shell is set to /bin/false. This setting is to prevent any other user on the system from logging in as that user, procuring a shell, and gaining permissions over the directories and files run by these system users.

> ### CAUTION
> Be careful when changing any user’s shell. You can inadvertently disable a user from logging in if the shell doesn’t exist. You should take extra caution when modifying root’s variables in any way.

Another method of preventing regular users from gaining access to certain daemons and other off-limits system processes is to create an unique user who owns the specific directories containing scripts and HTML files or unique daemons such as the httpd daemon. By using this method, you can avoid using the default nobody user by creating another dedicated system user with only limited permissions. Accounts such as webuser or www are good examples of users who should be given a default shell when used by other processes. This helps discourage users or intruders from exploiting weaknesses in the system.

# ## Shell Scripts

The shell itself is highly interactive. It can be used as a platform for creating unique scripts of commands to accomplish specific system tasks. The shell provides the environment for users to create these scripts and then run them from the command line. These scripts can either be initiated at the command prompt