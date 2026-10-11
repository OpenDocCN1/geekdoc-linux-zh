
35. Which of the following directories should be on their own partition? (Select all that apply.)
- A. /usr
- B. /boot
- C. /home
- D. /tmp

36. The ________ command provides an easy-to-use interface to Debian package management.

37. Which command(s) would be used to display which kernel packages are installed on your system?
- A. `rpm -ql | grep kernel`
- B. `rpm -qa | grep kernel`
- C. `dpkg -l kernel`
- D. `dpkg -l | grep kernel`

38. To use the X11 graphical interface to make a kernel configuration, you would use which of the following?
- A. `make gconfig`
- B. `make xconfig`
- C. `make menuconfig`
- D. `make tclconfig`

39. After editing the */etc/lilo.conf* file, you must run the ________ command.

40. If you want to remotely display an X Window application to another system, which option would you use?
- A. -display
- B. -connect
- C. -remote
- D. -xhost

41. You have a Red Hat system that currently boots in text mode. Which file do you need to modify to have it boot in GUI mode?
- A. /etc/runlevel
- B. /etc/init.conf
- C. /etc/inittab
- D. /etc/xdm

42. The ______ file stores the monitor information for X Window v4 (no path).

43. Which X11 application is known to have memory leaks?
- A. Netscape
- B. Internet Explorer
- C. Sawfish
- D. WindowMaker

44. The ______ command displays all e-mail messages waiting in the mail queue.

45. Given the following files, would the host norbert be allowed to connect to the FTP server?
```
hosts.deny:	in.ftpd : ALL
hosts.allow:	in.ftpd : norbert
```
- A. Yes
- B. No

46. Which type of modem is usually not compatible with Linux?
- A. Internal
- B. External
- C. Integrated
- D. Winmodem

47. You need to access a resource named Documents shared by the NFS server bigserver. Which command would you use?
- A. mount -t nfs //bigserver/Documents /mnt/docs
- B. mount bigserver:Documents /mnt/docs
- C. mount -t nfs bigserver:/Documents /mnt/docs
- D. nfs mount bigserver:/Documents /mnt/docs

48. After updating the /etc/exports file, the ______ command must be run for it to take effect (with option(s)).

49. When examining the network logs for the firewall, you notice a lot of connection attempts to port 110. Which service may your remote users be trying to use?
- A. IMAP
- B. DNS
- C. POP3
- D. SMTP

50. After editing the `/etc/modules.conf` file you should run the ________ command.

51. The first line of a shell script should be which of the following?
- A. `#!/bin/sh`
- B. `#!/bash`
- C. `#!/usr/bin/bash`
- D. `#!/bin/bash`

52. User application defaults are stored in which file?
- A. `.Xresources`
- B. `.Xdefaults`
- C. `.Xinit`
- D. `.xinitrc`

## Exam 101 Answers

- 1. A. Choice A would run `cmd1` and then `cmd2` regardless of the output of `cmd1`. Choice B would run `cmd1` sending the output to `cmd2`. Choice C would append the output of `cmd1` to the file `cmd2`. Choice D would send the output of `cmd1` to the file `cmd2`.

- 2. 15. The default signal used with the `kill` command is 15, `sigterm`.

- 3. C. Choice A, the `grep` utility, searches files for the specified expression. Choice B, the `find` utility, searches directories for files. Choice C, the `locate` utility, searches the `slocate` database. This database is updated using the `updatedb` command. Choice D does not search for files.

- 4. B. Choice A, the `jobs` utility, is used to view backgrounded processes. Choice B, `nice`, is used to change the priority of a process as it is run. Choice C, `renice`, is used to change the priority of a process before it is run. Choice D, `top`, is used to view process information.

- 5. D. Choice A would change the ownership of `myfile` if the userid of the new owner were specified. Choice B would change the permissions of `my_file` to `-rw-rw--x-x`. Choice C would change the permissions on `myfile` to `--wx-wx--x`. Choice D would change the permissions on `myfile` to `-rw-rw-r--`. 

- 6. A. The `/etc/passwd` file contains the user's home directory settings. Choice B, `/etc/skel`, contains files that are copied to all users' home directories. Choice C, `/etc/profile`, contains systemwide environment settings. Choice D, `/etc/bashrc`, contain global bash settings.

- 7. `crontab`. The `crontab` command is used to view jobs scheduled to run using `cron`.

8. C. Choice A does not follow the correct syntax for the `sed` command. Choice B would locate all instances of the letter *l* and replace them with *L*. Choice C would search for the word *lady* and replace it with *Lady*. Choice D would search for the word *lady* but would pipe it to the `tr` utility, not replace *lady* with *Lady*.

9. D. Choice A, `nice`, is used to set the priority of a process when it is run. Choice B, `renice`, would change the priority of a process after it has been run. Choice C, `ps -aux`, would view a snapshot of all running processes. Choice D, `top`, displays a real-time view of processes.

10. D. Choice A, /etc/proc/, is not valid. Choice B, /mnt, is simply a directory. Choice C, /etc/fstab, contains a listing of file systems that can be mounted at boot. Choice D, /etc/mtab, contains a listing of all currently mounted file systems.

11. B. Choice A, `echo`, can be used to view the assignment of environment variables. Choice B, `export`, makes the environment variable assignment available system-wide. Choice C, `cat`, is used to view the contents of a file. Choice D, `env`, is used to view all environment variables declared on the system.

12. D. Choice A uses an incorrect option for the `mv` command. Choice B would copy all files from /ME to /YOU and delete /ME, but directories would not be copied. Choice C would produce a syntax error because the last argument when moving a directory must be a directory name. Choice D would recursively copy the files and directories in /ME to /YOU, after which they would be deleted from /ME.

13. B. Choice A would create the xmaslist file from the contents of the list file while trying to create each line of the same length. Choice B would alphabetize the list, then number it and send the output to the xmaslist pipe. Choices C and D would produce errors because the in command and the files are used incorrectly.

14. C. Only Choice C is correct. The -9 signal is used to kill a process without allowing it to end gracefully. The default signal, used with answer A, is -15, sigterm, the now signal is not valid, and the -12 option is sigusr2.

15. A, C, and D. When creating a new partition for use, the fdisk utility is used to create the partition, the mkfs utility is used to format the partition, and the mount utility is used to mount the file system for use.

16. du. The du utility is used to display directory space usage information.

17. C. The quota command is used to view user quotas. The quotan command is used to enable quotas. The edquota command is used to edit disk quotas. The vi editor is started by the edquota command when editing quotas.

18. D. The umask of 002 would be used to filter the write permission for other users.

19. A. The /etc/shadow file must be readable by only the root user.

- 20. D. The shutdown command, when used alone, will switch to single-user mode. The telinit command can be used to change runlevels, with level 6 used for rebooting and level 0 used to halt or shut down the system.

- 21. A and D. The useradd command is used to create new user accounts while the passwd command is used to set the user's password.

- 22. B. The permissions of read and execute have a numeric value of 5 while the read permission has a value of 4.

- 23. C. The more utility is used to view a file one page at a time. The grep utility is used to search a file. The man utility is used to present manual pages that contain information about commands. The help utility displays information only for built-in commands.

- 24. /etc/skel. Files that are to be copied to each user's home directory should be placed in the /etc/skel directory.

- 25. C. The shell prompt is configured with the PS1 environment variable. The PATH variable is used for the command path while the home directory is contained in the HOME variable.

- 26. A, C, and D. The cd command, when used alone, changes the user's pwd to their home directory. The $HOME variable and the - also can be used to represent the user's home directory. The cd .. command is used to move up one directory in the directory tree.

- 27. C. The /etc directory contains many of the configuration files for the system. The /root directory is the home directory for the root user. The /sbin directory contains utilities used by the superuser. The /usr/local directory is used to store software that isn't part of the operating system.

- 28. B. The /etc/passwd file is used to store shell script assignments along with home directory assignments. The /etc/skel directory contains the files to be copied to each user's home directory. The /etc/profile file contains global user settings. The LILO boot loader is used to configure booting options.

- 29. D. The cp and mv commands can be used to relocate the files. Hard links cannot span file systems. Using soft links, you have the files appear to be stored on one file system while actually existing on another.

- 30. A. The userdel -r command is used to remove a user's home directory as well as their account. The usermod command can be used to disable a user's account. The passwd utility is used to change a user's password.

- 31. od. The od utility allows files to be viewed in octal and hexadecimal formats.

- 32. A. The grep utility is used to search a file for the specified string. The locate command searches the slocate database for specified files. The find command searches directories for the specified files. The where command is invalid.
