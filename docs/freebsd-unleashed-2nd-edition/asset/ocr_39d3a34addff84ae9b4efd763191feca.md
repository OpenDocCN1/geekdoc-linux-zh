# LISTING 10.2  Continued

```
hostname="freebsd1.testnetwork.com"
usbdo_enable="YES"
```

Some of these variables are, in fact, redundant with the defaults file; still, it can be useful to have them in the overrides file, as well, because many of these features (such as the NFS server) now have a one-turn toggle control, as it were.

Many programs, when you install them, will have to install a way for themselves to start up at boot time; /etc/rc.conf is not, however, the place for these programs. This file is supposed to be touched only by you, the administrator, and by the sysinstall program when it makes changes to the core system. Another structure, the /usr/local/etc hierarchy, is in place for the startup scripts and configuration files of user-installed programs (ports and packages) and for any scripts that /etc/rc and friends do not know about.

# The /usr/local/etc and /usr/local/X11R6/etc Directories

As you learned in Chapter 8, anything installed by the administrator goes into /usr/local. This is as true of startup scripts as it is of programs and shared libraries. The /usr/local/etc directory is the “local” equivalent of /etc (local referring to “this specific machine” as opposed to the generic components and settings found on all FreeBSD machines), and into it go all the configuration files installed by programs that you choose to install, rather than the ones controlled by the FreeBSD base system distribution.

> **NOTE**
> 
> It’s important to note that the difference between the /etc files and the /usr/local/etc files is not that the former are noneditable and the latter are editable. Just as most of the files in /etc should not be tampered with, many of the ones in /usr/local/etc also contain no user-serviceable parts or are designed not to need any modification by you in order to function (although the directory also contains customizable configuration files for installed programs). The distinction is that /etc controls the base system—for example, only those programs that are always part of a FreeBSD installation. The files in /usr/local/etc control programs that you install after the fact, from the ports collection or from packages (which you’ll learn about in Chapter 14, “Installing Additional Software”). /usr/local/etc also doubles as the location for any startup scripts you write.

The main local configuration directory, /usr/local/etc, contains configuration files that administrators edit to tune their programs’ behaviors. You learn more about configuring ports and packages in Chapter 14. Here, however, we’re interested in the rc.d (resource configuration for daemons) subdirectory.

init turns its attention to /usr/local/etc/rc.d after it has run through all the other /etc/rc.* or /etc/rc.d scripts. Any executable files within the directory that end in .sh are executed in lexicographical order. Examples of files that are installed in here include

![](bbox=[0.92, 0.78, 0.98, 0.88])