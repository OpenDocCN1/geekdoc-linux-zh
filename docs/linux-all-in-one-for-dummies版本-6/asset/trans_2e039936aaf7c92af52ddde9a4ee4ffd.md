
Here are the top ten items to know as you study for this domain:

- Regular expressions – often referred to as *globbing* – can be used with the shells available in Linux to match wildcard characters. Among the possible wildcards, the asterisk (*) matches any number of characters; the question mark (?) matches only one character.
- Linux is a case-sensitive operating system.
- Files can be hidden by preceding their names with a single period (.). In pathnames, however, a single period (.) specifies this directory, and two periods (..) signifies the parent directory.
- Absolute paths give the full path to a resource, whereas relative paths give directions from where you're currently working. An example of an absolute path is `/tmp/eadulaney/file`, and an example relative path is `../file`.
- Files can be copied by using `cp` or moved by using `mv`. Files can be deleted with `rm`, and directories (which are created with `mkdir`) can be removed with `rmdir`. Recursive deletion can be done with `rm -r`.
- To change directories, use the `cd` command. When this command is used without parameters, it moves you to your home directory. To see what directory you're currently working in, use the `pwd` (present working directory) command.
- The `ls` command has a plethora of options allowing you to list files. The `-a` option lists all files (including hidden files).
- Help is available through the manual pages (accessed with the `man` command) and `info` (which shows help files stored below `/usr/info`).
- The `whatis` command shows what manual pages are available for an entry, and `whereis` shows the location of the file and all related files (including any manual pages).
- Many standard utilities allow you to enter the name of the executable followed by "--help" to obtain help only on the syntax.

## The Power of the Command Line

Table 1-4 shows the subtopics, weights, descriptions, and key knowledge areas for this topic.

### TABLE 1-4 Breakout of Topic 3

| Subtopic | Weight | Description | Key Areas |
|---|---|---|---|
| Archiving Files in the Command Line | 2 | Archiving files in the user home directory | Files, directories, archives, and compression<br>(Topics include tar as well as common tar options, gzip, bzip2, zip, and unzip.) |
| Searching and Extracting Data from Files | 3 | Searching and extracting data from files in the home directory | Command-line pipes, I/O redirection, and basic regular expressions<br>(Topics include grep, less, cat, head, tail, sort, cut, and wc.) |
| Turning Commands into a Script | 4 | Turning repetitive commands into simple scripts | Basic shell scripting and awareness of common text editors<br>(Topics include #!, /bin/bash, variables, arguments, for loops, echo, and exit status.) |

Here are the top ten items to know as you study for this domain:

- `Standard input (stdin)` is traditionally the keyboard, and `standard output (stdout)` is traditionally the monitor. Both can be redirected, as can `standard error (stderr)`, by using the symbols >, >>, <, and |.
- Commands can be joined on the command line by the semicolon (;), and each command runs independently. You can also use the pipe (|) to send the output of one command as the input of another command.
- The `cut` command can pull fields from a file, and the fields can be combined by using either `paste` or `join`. The latter offers more features than the former and can be used with conditions.
- The `wc` command can count the number of lines, words, and characters in a file.
- The `grep` utility (and its counterparts `egrep` and `fgrep`) can be used to find matches for strings within files.
- The `find` command can be used to search the system for files/directories that meet any number of criteria. When these entities are found, the `xargs` command can be used to look deeper within them for other values (such as in conjunction with `grep`).
- You can use the `tar` command (which can combine multiple files into a single archive) to do backups.
- In addition to archiving, you can compress files with the `gzip` or `pack` command. To uncompress files, use `uncompress`, `gunzip`, or `unpack`.
- Variables can be given at the command line and referenced as $1, $2, and so on, or entered into the executing file with the read command.
- Logic can be added to scripts by testing conditions with test or [. Commands can execute through if-then-fi deviations or looping (while, until, or for). You can use the exit command to leave a script or use break to leave a loop.

## The Linux Operating System

Table 1-5 shows the subtopics, weights, descriptions, and key knowledge areas for this topic.

### TABLE 1-5 Breakout of Topic 4

| Subtopic | Weight | Description | Key Areas |
|---|---|---|---|
| Choosing an Operating System | 1 | Knowledge of major operating systems and Linux distributions | Windows, Mac, and Linux differences; distribution lifecycle management (Topics include GUI versus command line, desktop configuration; maintenance cycles, and Beta and Stable.) |
| Understanding Computer Hardware | 2 | Familiarity with the components that go into building desktop and server computers | Hardware (Topics include motherboards, processors, power supplies, optical drives, peripherals, hard drives and partitions, /dev/sd*, and drivers.) |
| Where Data Is Stored | 3 | Where various types of information are stored on a Linux system | Programs and configuration, packages and package databases, processes, memory addresses, system messaging, and logging (Topics include ps, top, free, syslog, dmesg, /etc/, /var/log, /boot/, /proc/, /dev/, and /sys/.) |
| Your Computer on the Network | 2 | Querying vital networking settings and determining the basic requirements for a computer on a local area network (LAN) | Internet, network, routers, querying DNS client configuration, and querying network configuration (Topics include route, ip route show, ifconfig, ip addr show, netstat, /etc/resolv.conf, /etc/hosts, IPv4, IPv6, ping, and host.) |

Here are the top ten items to know as you study for this domain:

- When run, every command spans at least one process; processes can be viewed with `ps` or `top` (which updates the display dynamically).
- Jobs can run in the foreground or background and be moved between the two. Jobs running in the foreground can be suspended by pressing Ctrl+Z.
- IPv4 uses 32-bit addresses, each divided into four octets. The first octet identifies the class of address (A, B, or C). The address can be public or private.
- The `ifconfig` utility can be used to see the current IP configuration of the network cards.
- The `ping` utility is an all-purpose tool for testing connectivity. It sends echo messages to a specified host to see whether that host can be reached. You can use `ping` with the loopback address (127.0.0.1) to test internal configuration.
- The `route` utility displays the routing table and allows you to configure it.
- The `netstat` utility shows the current status of ports – those that are open, listening, and so on.
- The system log is `/var/log/messages`, and this log is where the majority of events are written to by the system log daemon (`syslogd`). Messages routed there can be viewed with the `dmesg` command.
- The `logrotate` command can be used to automatically archive log files and perform maintenance as configured in `/etc/syslog.conf`.
- You can manually write entries to log files by using the `logger` command.

## Security and File Permissions

Table 1-6 shows the subtopics, weights, descriptions, and key knowledge areas for this topic.

Here are the top ten items to know as you study for this domain:

- File and directory permissions can be changed with the `chmod` command (which accepts numeric and symbolic values).
- Adding 1000 to standard permissions turns on the sticky bit; adding 2000 turns on the SGID permission. Adding 4000 turns on the SUID permission.

### TABLE 1-6 Breakout of Topic 5

| Subtopic | Weight | Description | Key Areas |
|---|---|---|---|
| Basic Security and Identifying User Types | 2 | Understanding various types of users on a Linux system | Root, standard, and system users<br>(Topics include /etc/passwd, /etc/group, id, who, w, sudo, and su.) |
| Creating Users and Groups | 2 | Creating users and groups on a Linux system | User and group commands, and user IDs<br>(Topics include /etc/passwd, /etc/shadow, /etc/group, /etc/skel, id, last, useradd, groupadd, and passwd.) |
| Managing File Permissions and Ownership | 2 | Understanding and manipulating file permissions and ownership settings | File/directory permissions and owners<br>(Topics include ls -l, ls -a, chmod, and chown.) |
| Special Directories and Files | 1 | Understanding special directories and files on a Linux system, including special permissions | Using temporary files and directories, and symbolic links<br>(Topics include /tmp, /var/tmp, Sticky Bit, ls -d, and ln -s.) |

- Links are created with the `ln` command. A *hard link* is nothing more than an alias to a file (sharing the same inode). The `ln -s` command creates a symbolic link that's an actual file with its own inode. The symbolic link contains a pointer to the original file and can span file systems; the hard link can't.
- User accounts can be added by manually editing the configuration files or using the `useradd` command; they can be removed with `userdel`.
- The `groupadd` utility can be used to create groups, and `groupdel` can be used to remove groups. Groups can be modified with `groupmod`, and users can be moved from one group to another with the `newgrp` command.
- Passwords are changed with the `passwd` command. Older systems stored passwords in `/etc/passwd`; now passwords are stored in `/etc/shadow`, where they're more secure.
- To see who logged on most recently and may still be on the network, you can use the `last` command.
