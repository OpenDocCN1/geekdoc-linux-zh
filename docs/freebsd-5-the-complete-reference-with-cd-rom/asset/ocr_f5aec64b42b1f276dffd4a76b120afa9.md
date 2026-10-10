you want to adjust and changing that call. (In this context, a *call* is a reference to a program that causes that program to run. It might be nothing more than the name of the program on a line in the script.)

> **Caution**
> *Modifying the FreeBSD startup scripts is a potentially dangerous undertaking. If you err, the computer may not boot at all. What's worse, you may not realize you've made an error until days, weeks, or even months later. If you don't reboot your computer immediately after making a change, I recommend you make a backup of any system startup script before you modify it, and reboot immediately after making the change. If the system then fails to boot, you can use an emergency system to restore the original file or try again.*

You might edit two other files or file classes to alter the startup routine: the * `/etc/rc.local` *script and scripts in the `/usr/local/etc/rc.d` directory. Both are designed to accept customizations, but the second is the favored tool in recent versions of FreeBSD. Chapter 6 describes customizing these scripts in more detail.

> **Note**
> *Both the /etc/rc.local file and the /usr/local directory names contain the word local. This word refers to the system-specific nature of the programs or files referenced or contained therein, as contrasted with standard tools that can be found on most FreeBSD systems.*

# ### Server Configuration Files

A second class of configuration files found in `/etc` are those related to specific servers. Many of these files are covered in greater detail in subsequent chapters of this book, and particularly in Part IV. As a quick introduction and so that you know what some of these files are, here are several of the more important server configuration files and directories:

+   * **X files** The `/etc/XF86Config` file and `/etc/X11` directory control the XFree86 X server and affiliated programs, such as the X Display Manager (XDM) GUI login program. Chapter 13 covers the XF86Config file in more detail.

+   * **Apache files** The `/usr/local/etc/apache` directory contains files for configuring the popular Apache web server. Most importantly, `httpd.conf` is the main configuration file; other files in the directory are support files. Chapter 20 covers the basics of Apache configuration.

+   * **`/etc/exports`** This file specifies directories that FreeBSD is to make available via the Network File System (NFS) file server, as described in Chapter 18.

+   * **TCP Wrappers files** The TCP Wrappers program is an important security package used by many servers. It uses the `/etc/hosts.allow` and `/etc/hosts.deny` configuration files. This package is described in Chapter 29.