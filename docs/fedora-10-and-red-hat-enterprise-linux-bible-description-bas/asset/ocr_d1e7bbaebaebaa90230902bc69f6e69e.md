# Administrative configuration files

Configuration files are another mainstay of Linux administration. Almost everything you set up for your particular computer — user accounts, network addresses, GUI preferences — is stored in plain-text files. This has some advantages and some disadvantages.

The advantage of plain-text files is that it is easy to read and change them. Any text editor will do so. On the downside, however, is that you edit configuration files, no error checking is going on. You have to run the program that reads these files (such as a network daemon or the X desktop) to find out if you set the files correctly. A comma or a wrong place can sometimes cause you to hit a faulty interface.

Throughout this book, I describe the configuration files you need to set up the different features that make Fedora and RHEL systems. In terms of a general perspective on configuration files, however, there are several locations in a Fedora or RHEL file system where configuration files are stored. Here are some of the major locations:

+   $HOME — Users store information in their home directories that directs how their login accounts behave. Most configuration files in $HOME begin with a dot (.), so they don't appear as a user's directory when you use a standard ls (command you need to type ls -a to see them). There are files that define how your shell behaves, the desktop look and feel, and options with your text editor. There are even files (such as .ssh/* and .hosts) that can configure network permissions for each user.
/etc — This directory contains most of the basic Linux system-configuration files. The following /etc configuration files are of interest:
    * adjtime — Holds data to adjust the hardware clock (see the hwclock page).
* aliases — Can contain distribution lists used by the Linux mail service.
* bashrc — Sets system-wide defaults for bash users (By default, it sets the prompt to include current user name, hostname, current directory, and other values).
* cdrecord.conf — Contains defaults for recording CDs.
* crontab — Sets environ and times for running automated tasks.
* csh.shrc (or cshrc) — Sets system-wide defaults for csh (C shell) users.
* docot — Contains information needed to support the docot IMAP4/POP3 mail service.
* esd.conf — Sets options used by the Enlightenment Sound Daemon to manage multiple audio streams into a single audio output.
* exports — Contains a list of local directories that are available to be shared by remote computers using the Network File System (NFS).
* fedora-release — Contains a string identifying the current Fedora release. For RHEL, the file is named redhat-release.