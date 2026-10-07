# CHAPTER 5 First Steps with Linux

The only time you should run Red Hat Linux as the superuser is when booting to runlevel 1, or system maintenance mode, to configure the filesystem, for example, or to repair or maintain the system. Logging in and using Linux as the root operator isn't a good idea because it defeats the entire concept of file permissions.

Knowing how to run commands without logging in as root can help avoid serious mistakes when configuring your system. Red Hat Linux comes with a command sudo that allows you to run one or more commands as root and then quickly return to a normal user status. For example, if you'd like to edit your system's filesystem table (a simple file that describes local or remote storage devices, their type, and location), you can use the sudo command like:

```
$ su -c "vi /etc/fstab"
```

Password:

After you press Enter, you'll be prompted for a password that gives you access to root. This extra step can also help you “think before you leap” into the command. Enter the root password, and you'll be editing /etc/fstab using the pico editor with line wrapping disabled.

> CAUTION

> Before editing any important system or software configuration file, make a backup copy. Then make sure to launch your text editor with line wrapping disabled. If you edit a configuration without line wrapping, you could insert spurious carriage returns and feeds into its contents, causing the configured service to fail when restarting. By convention, nearly all configuration files are formatted for 80-character width, but this isn't always the case. By default, the vi and emacs editors don't use line wrap.

You can use sudo to assign specific users permission to perform specific tasks (similar to BSD UNIX and its “wheel” group of users). The sudo command works by first examining the file named sudo /etc directory; you modify this file with the visudo command. See the section “Granting Root Privileges on Occasion—The sudo Command” in Chapter 9, “Managing Users,” for details on how to configure and use sudo.

# Creating Users

When a Red Hat Linux system administrator creates a user, an entry in /etc/passwd for the user is created. The system also creates a directory, labeled with the user’s username, in the /home directory. For example, if you create a user bsmith, the user’s home directory is /home/bsmith.

> NOTE

> In this chapter, you learn how to manage users from the command line. See Chapter 9, “Managing Users,” for more information on user administration with Red Hat Linux using graphical administration utilities, such as the redhat-config-users client.