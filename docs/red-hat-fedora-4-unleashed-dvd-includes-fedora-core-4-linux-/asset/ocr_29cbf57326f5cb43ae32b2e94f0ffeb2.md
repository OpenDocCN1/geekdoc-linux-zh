When you work in root, you have the ability to destroy a running system with a simple invocation of the rm command like this:

```
# rm -fr /
```

This command line will not only delete files and directories, but also could wipe out file systems on other partitions and even remote computers. This alone is reason enough to take precautions when using root access.

The only time you should run Linux as the superuser is when booting to runlevel 1, or system maintenance mode, to configure the filesystem, for example, or to repair or maintain the system. Logging in and using Linux as the root operator isn't a good idea because it defeats the entire concept of file permissions.

Knowing how to run commands as root without logging in as root can help avoid serious missteps when configuring your system. Linux comes with a command named su that allows you to run one or more commands as root and then quickly return you to normal user status. For example, if you would like to edit your system's filesystem table (a simple text file that describes local or remote storage devices, their type, and location), you can use the su command like this:

```
$ su -c "nano -w /etc/fstab"
Password:
```

After you press Enter, you will be prompted for a password that gives you access to root. This extra step can also help you “think before you leap” into the command. Enter the root password, and you will then be editing /etc/fstab using the nano editor with line wrapping disabled.

> **CAUTION**
> 
> Before editing any important system or software service configuration file, make a backup copy. Then make sure to launch your text editor with line wrapping disabled. If you edit a configuration file without disabling line wrapping, you could insert spurious carriage returns and line feeds into its contents, causing the configured service to fail when restarting. By convention, nearly all configuration files are formatted for 80-character text width, but this is not always the case. By default, the vi and emacs editors don't use line wrap.

You can use sudo to assign specific users permission to perform specific tasks (similar to BSD Unix and its “wheel” group of users). The sudo command works by first examining the file named sudoers under the /etc directory; you modify this file with the visudo command. See the section “Granting Root Privileges on Occasion—The sudo Command” in Chapter 13, “Managing Users,” for details on how to configure and use sudo.

# ## Creating Users

When a Linux system administrator creates a user, an entry in /etc/passwd for the user is created. The system also creates a directory, labeled with the user's username, in the /home