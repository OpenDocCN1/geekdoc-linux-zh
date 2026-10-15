
## Configuration Files and Tools

After you’ve done the basic installation on your system, you’ll probably need to modify that configuration to suit your exact needs. In some sense, that’s the topic of this entire book, although this book covers only a subset of Linux configuration issues. There are commonalities to most Linux configuration procedures, though, and being familiar with them can help you, both in setting up a Linux server and in other Linux configuration tasks.

## The /etc Directory and Its Contents

Linux’s configuration is done through text files, not binary registry files, as in Windows. Linux stores its configuration files in the /etc directory or subdirectories off /etc. This may sound simple enough, until you take a look at the /etc directory’s contents and see the dozens of files there! Here’s a rundown of some of the most important files and directories in /etc:

- X11/ — This is a subdirectory that contains files for configuring XFree86, the most important of these files being XF86Config.
- atalk/ — Netatalk configuration files reside in this directory. It won’t exist on a fresh Red Hat install, however.
- conf.modules — You can provide information on how Linux loads and uses device driver modules in this file.
- cron.*/ — Several subdirectories beginning with cron are used to configure the Linux cron feature. This feature lets you run programs at specified intervals, and it’s used to help clean up system files and temporary directories, among other things.
- fstab — This file controls how Linux mounts its partitions. You’ll need to modify it if you add or delete partitions or removable disks, or if you want to modify how an existing partition is handled.
- group — Linux collects users into groups of users, and the group file specifies which users belong to which groups.
- hosts — This file lists the host names and IP addresses of frequently accessed computers.
- hosts.allow — For network services that are controlled by the TCP Wrappers utility, you can specify the computers that are allowed to access the service in the hosts.allow file. Use this if you want to provide a service to only a limited number of computers.
- hosts.deny — If there are computers or domains you want to explicitly forbid from using a service, place them in the hosts.deny file.
- inetd.conf — This is the configuration file for the inetd daemon. It’s a very important file for Linux networking because many distributions (including Red Hat) use inetd to launch specific daemons when they’re needed and not before.
- inittab — The inittab file controls many aspects of the boot process, specifying which other files in /etc are run and in what order.
- ld.so.conf — Linux searches for libraries (files with code that’s often shared between programs) in certain directories specified in this file.
- lilo.conf — The configuration for the LILO utility is stored here. If you change this file, you must reinstall LILO by typing lilo.
- passwd — Usernames and associated information, sometimes including their passwords, are stored in this file.
- printcap — This file defines your printer queues.
- profile — Environment variables and startup programs common to all users are stored here.
- services — This file lists standard services and their port numbers. Just because a service is listed in this file does not mean it’s available on your system, though.
- shadow — If you enable shadow passwords, users’ passwords are stored here rather than in the passwd file. The passwd file is still used for most user information, though. The idea is that the shadow file can have more restrictive permissions than can the passwd file, and so an uninvited guest won’t be able to obtain users’ passwords, even in an encrypted form.
- smb.conf — Samba configuration information is stored here.

This is by no means an exhaustive listing of the files in the /etc directory, as you know if you’ve taken a look and compared what you saw to what I’ve just listed. These are some of the most important files, however, especially for a Linux file and print server.

## Using linuxconf

If you’re new to Linux and UNIX, you might feel intimidated by the need to edit text files to configure your OS. That’s one of the reasons Red Hat developed linuxconf, a utility to configure a Red Hat Linux system using a textual or graphical user interface rather than a text editor and manuals. You normally have to be root to run linuxconf. When you do, the program checks your environment and runs in full GUI mode when you’re running in X (see Figure 5.8), or in text-only mode if you’re not.
