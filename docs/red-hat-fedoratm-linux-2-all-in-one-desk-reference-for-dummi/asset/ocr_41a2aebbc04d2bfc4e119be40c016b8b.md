| Subdirectory | Description |
| :--- | :--- |
| `/usr/local` | Contains local files. The `/usr/local/bin` directory, for example, is supposed to be the location for any executable program developed on your system. |
| `/usr/sbin` | Contains many administrative commands, such as commands for electronic mail and networking. |
| `/usr/share` | Contains shared data, such as default configuration files and images for many applications. For example, `/usr/share/gnome` contains various shared files for the GNOME desktop; and `/usr/share/doc` has the documentation files for many Linux applications (such as the Bash shell, the Sawfish window manager, and the GIMP image-processing program). |
| `/usr/share/man` | Contains the online manual (which you can read by using the `man` command). |
| `/usr/src` | Contains the source code for the Linux kernel (the core operating system). |

# Table 3-3 Important `/var` Subdirectories

| Subdirectory | Description |
| :--- | :--- |
| `/var/cache` | Storage area for cached data for applications. |
| `/var/lib` | Contains information relating to the current state of applications. |
| `/var/lock` | Contains locked files to ensure that a resource is used by one application only. |
| `/var/log` | Contains log files organized into subdirectories. The syslogd server stores its log files in `/var/log`, with the exact content of the files depending on the syslogd configuration file `/etc/syslog.conf`. For example, `/var/log/messages` is the main system log file, `/var/log/secure` contains log messages from secure services (such as `sshd` and `xinetd`), and `/var/log/maillog` contains the log of mail messages. |
| `/var/mail` | Contains user mailbox files. |
| `/var/opt` | Contains variable data for packages stored in `/opt` directory. |
| `/var/run` | Contains data describing the system since it was booted. |
| `/var/spool` | Contains data that's waiting for some kind of processing. |
| `/var/tmp` | Contains temporary files preserved between system reboots. |
| `/var/yp` | Contains Network Information Service (NIS) database files. |

# ## Navigating the File System with Linux Commands

Although GUI file managers such as Nautilus (in GNOME) or Konqueror (in KDE) are easy to use, you can use them only if you have a working GUI