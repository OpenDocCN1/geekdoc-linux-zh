# /usr/local in Red Hat Linux

In Red Hat Linux, the intended use for /usr/local is slightly different from that specified by the FSS TND. The FSS TND says that /usr/local should be where you store software that is to remain safe from system software upgrades. Since system upgrades from Red Hat Software are done safely with the RPM system and GnoRPM, you don't need to protect files by putting them in /usr/local. Instead, we recommend you use /usr/local for software that is local to your machine. For instance, let's say you have mounted /usr via read-only NFS from beavis. If there is a package or program you would like to install, but you are not allowed to write to beavis, you should install it under /usr/local. Later perhaps, if you've managed to convince the system administrator of beavis to install the program on /usr, you can uninstall it from /usr/local.

# Special Red Hat File Locations

In addition to the files pertaining to the RPM system that reside in /var/lib/rpm (see Chapter 9), there are two other special locations that are reserved for Red Hat Linux configuration and operation.

The control-panel and related tools put lots of stuff in /usr/lib/rhs. There is probably nothing here that you would want to edit. It is mostly small scripts, bitmaps and text files.

The other location, /etc/sysconfig, stores configuration information. The major users of the files in this directory are the scripts that run at boot time. It is possible to edit these by hand, but it would be better to use the proper control-panel tool.

# Users, Groups and User-Private Groups

Managing users and groups has traditionally been tedious. Red Hat Linux has a few tools and conventions that make users and groups easier to manage, and more useful. The easiest way to manage users and groups is through Linuxconf (see Chapter 8). However, you can also use adduser to create a new user from the command line.