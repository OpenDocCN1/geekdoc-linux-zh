# # Using the root User Account

The traditional role of the root user in Linux systems is to have complete control of the operation of your system. That user can open any file or run any program. The root user also installs software packages and adds accounts for other people who use the system.

During the CentOS installation process, you are required to add a password for the root user. You need to remember and protect this password. You will need it to log in as root or to obtain root permission while you are logged in as some other user.

The home directory for the root user is /root. The home directory and other information associated with the root user account is assigned in the /etc/passwd file. Here is what the root user’s entry looks like in the /etc/passwd file:

```
root::x:0:0:root::/root::/bin/bash
```

This shows that for the user named root, the x indicates that the password is stored in /etc/shadow, the user ID is set to 0 (root user), and the group ID is set to 0 (root group). The home directory is /root, and the shell for that user is /bin/bash.

> **CROSS-REF:** It’s best to make changes to /etc/passwd with the User Manager window or usermod command. See the section on setting up users in Chapter 10 for more information about the /etc/passwd file.

Among the defaults that are set for the root user are aliases for certain commands that could have dangerous consequences. Aliases for the rm, cp, and mv commands allow those commands to be run with the -i option. This prevents massive numbers of files from being removed, copied, or moved by mistake. The -i option causes each deletion, copy, or move to prompt you before removing or overwriting any files from those commands.

# ## Becoming the Super User (the su Command)

Although one way to become the super user is to log in as root, sometimes that is not convenient. For example, you may be logged into a regular user account and just want to make a quick administrative change to your system without having to log out and log back in. Or you may need to log in over the network to make a change to a Linux system but find that the system doesn’t allow root users in from over the network (a common practice).

The answer is that you can use the su command.

> **CAUTION:** In general, it is safer to use the sudo command to run a single Linux command as the super user instead of running the su command. See the description of the sudo command later in this chapter.