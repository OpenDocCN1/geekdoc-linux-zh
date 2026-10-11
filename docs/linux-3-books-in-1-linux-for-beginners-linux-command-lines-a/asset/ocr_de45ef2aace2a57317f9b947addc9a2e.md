# Chapter Two

# Securing User Accounts on Linux

# Don’t Login Using a Root Account

The root user on your Linux operating system is like the administrator user on Windows. There are situations where you may want to log in to the administrator account on Windows. You should never log in to Linux using the root account or user. Microsoft has worked on improving the security practices followed on Windows using user access control (UAC). Linux does not have any such tools readily available, so you should avoid using the root user.

# Using Sudo Accounts

Users need to avoid using the root account to access the operating system. Ubuntu gives sudo access to different users. Ubuntu locks the root account, so any user cannot log in to the root account without going out of his way to enable the root account and obtain the password.

Earlier versions of Linux distributions allowed users to access the root account through the graphical login screen. They can get to the root desktop. Many applications may not run as root applications, while others may throw errors. If you are moving from using Windows to Linux, you may want to log in to the operating system using root. You may think this is no different from using an administrator account on Windows. This is a terrible thing to do since it endangers your system.

When you use sudo accounts on Ubuntu, you get root privileges. If you use su, you only access the root shell to run the command you may need to use before you come out of the root shell. Through sudo, you can enforce the right security practices in your system. These accesses also ensure that you run the command as a root user without exiting the root shell. You can access and run an application as a root user only when you are in the root shell.