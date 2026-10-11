
33. D. The & character is used to background a process when it is run. The fg command is used to bring a process to the foreground. The bg command is used to background a suspended process. The Ctrl+Z sequence can be used to suspend a foreground process.

34. B. Man pages can be used to discover more information on commands and utilities. The HOWTOs contain information on configuring specific software and hardware. The /usr/doc directory contains information on installed applications. The dmesg command is used to display system messages.

35. B. The & character is used when running a process to specify that it runs in the background.

36. C. The HOME variable stores the user’s home directory. The PS1 variable stores the command prompt settings. The PATH variable contains the paths to search when running commands. The TERM variable stores the terminal setting.

37. chown. Ownership of files and directories is changed using the chown command.

38. A. The dmesg command is used to view system messages. Neither messages nor errors is a valid command. The lilo command is used when updating boot loader options using the /etc/lilo.conf file.

39. B. Only the tar utility is capable of creating an archive while compressing the file. The gzip, compress, and bzip2 utilities are used to compress and uncompress files.

40. D. The dmesg command is used to view system messages. The ls command is used to view directory contents. The bg command is used to run a process in the background. The jobs command is used to view jobs running in the background.

41. C. The tac utility displays files in reverse. The cat utility is used to display file contents. The head utility is used to view the beginning of a file. The top utility is used to view real-time information on system processes.

42. C. Stop limits and max limits are invalid. Soft limits can be exceeded for a period of time, while hard limits prevent a user from creating new files.

43. B. Runlevel 0 is used to halt the system; level 1 is used to enter single-user mode; level 3 can vary according to the distribution; and level 5 is used to reboot the system.

44. C. The /etc/fstab file contains file system information. The /etc/passwd file contains information on user accounts. The /quota.user file contains quota information for users. The /lilo file is invalid.

45. D. The man page can be specified using the syntax man NUMBER command. This correct syntax is shown as man 3 syslog.

46. D. The cat, more, and less utilities are all used to view file contents. The expand utility is used to convert tab characters to spaces.

47. umount. File systems are unmounted using the umount command.

48. history. The history command allows you to view previously entered commands.

49. B. The Web site www.deja.com enables you to search Usenet postings.

50. A. The /proc directory is virtual. It is used to store information about system resources and processes.

51. fscck. The fscck utility is used to verify and correct problems on file systems.

52. A. The -R option specifies that a recursive directory listing be performed. Data is sent to a file when the > symbol is used for redirection.

## Exam 102 Answers

1. mkfs. The mkfs tool is used to create a file system.

2. C. The -r parameter on lilo specifies a different root directory. This is used when you are doing recovery and /etc and /boot are actually mounted under a new root.

3. ld.so.conf. Whenever a new library is added manually, you must edit the ld.so.conf file and run ldconfig.

4. B. The -e parameter is used to remove a package with RPM. The other choices install packages.

5. B. By default, kernel configuration options are stored in the .config file.

6. D. The -qf parameters tell RPM to query (-q) the database to see who owns a certain file (-f).

7. ~/.bashrc or /etc/bashrc. The bashrc script is executed when a bash shell is started, but not when logging in. For example, if you open a new xterm in X11 with bash, this script will run.

8. A. traceroute is used to show the path a packet takes to a destination. The ping command tells you only if a remote host is up, and the route command is used to modify the local routing table.

9. C. The whois command shows contact information relating to a domain. The nslookup and dig tools are used to check DNS information. The whoinfo command is invalid.

10. A and C. When a change is made to in.dns.conf, the daemon must be restarted by either using the script or issuing a HUP.

11. /etc/nologin. This file causes the system to disallow all nonroot logins.

12. C and D. The pwconv and grpconv tools convert the passwd and group files to use shadow passwords. The other commands are fake.

13. A, C, and D. All three methods can be used to uncompress the file. The tar command does support gzip, but is used only when uncompressing a tar file.

14. swapon -a. The swapon -a command enables all swap partitions in the /etc/fstab file.

15. C. The last command shows the utmp file by default, and the who command uses the wtmp file. The other two commands are invalid.

16. D. The Apache package includes the apachecl tool to manage the httpd daemon. The other answers are invalid.

17. A. The lpq tool is used to manage and view the print queue, while lpc is used to manage the printing system. The lpq -a command will display information for all local printers. The printq command is invalid.

18. C. Disk Druid is a GUI tool supplied by Red Hat. Answers A and B provide text interfaces. Answer D is invalid.

19. lsmod. The lsmod command displays all loaded modules.

20. D. The forward slash tells vi to search the file for the given expression. The s command is used for substitution, while the f command searches for a single character in the current line. Answer C is invalid.

21. B. Any time an alias is added, the newaliases command needs to be run. Answers A and C are invalid. Restarting the sendmail process will not activate the new aliases.

22. A. Choice B is invalid due to the subnet mask. Choice C allows anyone from a .org domain to have access. The ALL wildcard is invalid as well.

23. D. The .xinitrc script is run from your home directory when startx is called. The other script names are invalid.

24. C. The ifconfig command is used to configure an interface, not a route.

25. B. Only root can change /etc/aliases. Answers C and D are invalid.

26. A. The smbd daemon handles file and printer sharing. Answer C is invalid. The named daemon is used to provide DNS.

27. su. The su, or substitute user, command is used to change to another user while logged in.

28. C. Choice A allows anyone to connect, which is a security risk. The X server does not use the rhosts file. Choice D is invalid.

29. C. The lower the number is, the higher the priority of the mail server.

30. B. The cp tool only works locally. Choice C uses the wrong path name, and choice D has incorrect syntax.

31. A. The update command is first used to update the available package list, and then the upgrade command is used to actually upgrade the packages.

32. 25. The SMTP protocol uses port 25.

33. pnpdump. This tool is used to scan the system and output any Plug-and-Play information to a text file for configuration.

34. C and D. IP Masq is not functioning since the rule must be set in the Forward chain. The second line enables IP forwarding.

35. A, B, C, and D. In most cases all of the directory structures should have their own partition for security and fault tolerance.

36. dselect. The dselect tool is an easy-to-use front end for dpkg.

37. B and D. Answer A is invalid, since no query string is present. Answer C will only display a package with the exact name “kernel”.

38. B. Answers A and D are invalid. The make menuconfig command provides a text mode menu.

39. lilo. You must rerun lilo after editing /etc/lilo.conf so that a new boot record is written with the updated information.

40. A. The -display parameter tells the application where to connect to for its output display. The other answers are invalid.

41. C. The inittab file tells the system which runlevel to boot to by default. In Red Hat, runlevel 3 is text mode and runlevel 5 is GUI mode. The other answers are invalid.

42. XF86Config-4. XFree86 v3 uses the XF86Config file.

43. A. Netscape is known to have stability problems and memory leaks.

44. mailq. The mailq command shows all messages in the mail queue, as well as any errors that may keep the messages from being delivered.

45. A. While the hosts.deny rule blocks everyone, the hosts.allow rule overrides it.

46. D. Winodems use software to handle most of their functionality, which is not supported in Linux due to lack of information from which to write drivers.

47. B. The mount command uses the syntax server:share mount_point for NFS shares.

48. exportfs -a. The exportfs command is used to control the directories shared via NFS. The -a option tells exportfs to share or unshare all configured directories.

49. C. IMAP uses port 143, DNS uses port 53, and SMTP uses port 25.

50. depmod. The depmod command sets up the module dependency links.

51. D. The other answers are invalid.

52. B. The Xdefaults file lists the default settings for X applications, as configured by the user. The xinit and xinitrc scripts are used to start X.

![](img/96d9ccd181675a8ae8b6a1146c919d2b_806_0.png)
