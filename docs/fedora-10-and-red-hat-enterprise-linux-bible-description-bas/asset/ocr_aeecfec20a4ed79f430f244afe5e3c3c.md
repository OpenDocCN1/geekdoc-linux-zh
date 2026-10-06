# Part III: Administering Fedora and RHEL

> CAUTION: If you are the administrator for a computer that is accessible to multiple users, don't leave a root shell open on someone else's screen (unless you want to let them do anything they like to the computer!)

Besides using a session su (to run a bunch of commands as root), you can instead use root permission to a single command or window. This approach is more secure than leaving a shell open with root permission if you are just doing one administrative task. For example:

+   **GUI admin tools** — When you run GUI administration tools as a regular user, you are usually prompted for the root password (as described the section "Using graphical administration tools" later in this chapter). If a GUI administration tool fails and doesn't prompt you for a password, refer to the sidebar "Becoming Super User in X."
**sudo command** — You can run the sudo command to configure a user in /etc/sudoers to be allowed to run administrative commands. After that is done, you can run the sudo command, followed by a single administrative command, to run that command as root. When single command completes, the root permission to run that command ends as well. (See the description

# Learning Administrative GUI Tools, Commands, Configuration Files, and Log Files

Fedora and Red Hat Enterprise Linux systems have advanced much in recent releases that you can now do system administration from your desktop GUI, bypassing the shell altogether. Whether you administer Linux from the GUI or from a shell, however, underlying your activities are many administrative commands, configuration files, and log files.

Understanding where GUI administrative tools, commands, and files are located and how they are used will help you effectively maintain your Linux system. Although most administrative features are intended for the root user, other administrative users (described later in this section) have limited administrative capabilities.

# Using graphical administration tools

The trend over the past few versions of Fedora and Red Hat Enterprise Linux has to steer clear of the messy administrative interfaces (such as linuxconf and Webmin) and instead to offer graphical windows that perform individual administrative tasks. Instead of sharing one monolithic interface, they share common menus. Individual graphical windows for configuring a network, adding users, or setting up printers can be launched from those menus.