Once the system is up and running in single-user mode, if you supply the correct password, you will be superuser. If the system comes up in multiuser mode, you can log in as root, and again, if you have the correct password, you can be superuser. You can also give the su command while you are logged in as yourself. If you know the appropriate password, you will have superuser privileges.

> **TIP** If you use the official system version of su, always specify su’s absolute path name, such as /usr/bin/su, when you use it.

Many of the commands used by superuser are kept in the /usr/bin directory. You can execute these commands by giving their full path names on the command line or by including the /usr/bin directory in your PATH when you are logged in as superuser. You can also make changes to the console line in the /etc/default/login file and control where root is allowed to log directly in to. No matter what is in this file, you can log in on the machine as an ordinary user and then use su to become root. This is a good setup for computers that are accessible to the public. With no root login available on the console, it will not matter if your machine is accessible. No one will be able to log in to the root account from the console. You will have to have a valid account on the computer before you can attempt to obtain superuser privileges. Change the line that begins with CONSOLE to read as follows:

```
```
# root cannot login directly on any device
CONSOLE =
```
```

If you are going to allow root to log in directly on the console, edit the /etc/default/login file and make sure the line beginning with CONSOLE is not commented out, as in the following example:

```
```
# root can log in on console
# CONSOLE=/dev/console
```
```

If the machine is in a server room or a locked space where only trusted people have access to it, this type of access is permissible. However, even a server room should have additional physical security such as locked doors with coded key pads.

> **WARNING** Never allow root access over the Internet. If you comment out the CONSOLE line in the /etc/default/login file, you allow root to log in on the machine directly over the network, possibly by using Telnet. Do not allow this kind of root access to any machine connected to the Internet.