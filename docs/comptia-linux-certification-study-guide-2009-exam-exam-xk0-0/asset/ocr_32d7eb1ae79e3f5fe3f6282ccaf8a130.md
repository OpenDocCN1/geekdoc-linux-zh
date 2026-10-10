+   ■ *Base repository* contains the Fedora release, usually on your installation media.
+   
+   ■ *Updates* will have all the updates from the base package.
+   
+   ■ *Extras* is a large selection of additional software that a user may want to install.

In addition there are also development repositories available which will have the newest code, but which may not be stable. Like `rpm`, `yum` needs to have superuser privileges to be performed. The available package groups provided by the Fedora repositories can be queried using `yum` using the command `su -c "yum grouplist"` and entering the superuser password when prompted. Part of the output can be seen below:

```
$ su -c 'yum grouplist'
Password:
Loaded plugins: refresh-packagekit
Setting up Group Process
Installed Groups:
 Administration Tools
 Base
 Dial-up Networking Support
 Engineering and Scientific
 Fonts
 GNOME Desktop Environment
 Games and Entertainment
 Graphical Internet
 Graphics
 Hardware Support
 Input Methods
```

> **Note**
> 
> As the root user, you have extreme power and can add and delete files, and mistakes can be made. Managing a Linux system can be achieved without logging in as root, but running them using a substitute user or switch user command (`su` or `sudo`) depending on the Linux distribution you are using.

# Installing Software with Yum

You can install new software packages or package groups with `yum`. The following show the commands for a single package (Firefox) and a package group (MySQL database):