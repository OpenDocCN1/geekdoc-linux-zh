
46. Answer D is correct because quotas are on a file system—by–file system basis and conflicting quotas cannot be configured on the same partition. Answer A is incorrect because they don’t have to be on separate drives, just separate file systems. Answer B is incorrect because the special bit 4 (SUID) has nothing to do with this situation. Answer C is incorrect because there is no /etc/qtab file on a standard Linux system.

47. Answer B is correct because the reserved percentage is set with the -m option followed by a percentage value in numerals. Answer A is incorrect because it’s a description of the targetfile option, which isn’t specified. Answer C is incorrect because the ext2 file system doesn’t do journaling, so metadata isn’t journaled. Answer D is incorrect because the description is indicative of the -M option’s behavior.

48. Answer A is correct because a Red Hat machine has the /etc/passwd file set to 644 and the /etc/shadow file set to 400. All other answers are wrong because of either permission being set incorrectly.

49. Answer: quota (There are no alternative correct answers.)

50. Answer D is correct because a Debian machine has the /etc/passwd file set to 644 and the /etc/shadow file set to 640. All other answers are wrong because of either permission being set incorrectly.

51. Answers A and D are correct because the /usr directory tree contains mostly binaries and reference files and the /dev directory tree is mostly static after the server is set up properly. Answer B is incorrect because anytime a user is added or a service is configured, the /etc directory is changed and the server is a busy system. Answer C is incorrect because, if there are any users at all, the /home directory changes frequently. Answer E is incorrect because the root user’s home directory can change frequently, and on a busy system you’ll spend a good amount of time as the root user.

52. Answer A is correct because a umask of 007 creates files with the permissions set to 660 by default. Answer B is incorrect because 022 is the default and creates files that are set to 644. Answer C is incorrect because it creates files that are too restrictive—they should be set to 640. Answer D is incorrect because a umask of 054 produces files that have permissions of 622.

53. Answer D is correct because the bash ulimit option is capable of restricting a user’s ability to create files above a certain size. Answer A is incorrect because the umask only has to do with masking out permissions. Answer B is incorrect because unalias is used solely to remove aliases. Answer C is incorrect because the noclobber option is for restricting a user’s ability to overwrite existing files with > redirection. Answer E is incorrect because unset is for removing arrays that have been set.

54. Answer C is correct because the `df` command, when used with the `-i` option, shows the number of used and free inodes for all mounted file systems. Answer A is incorrect because the `du` command shows information only about files on a file system, not file systems. Answer B is incorrect because the `fsck` command is capable of warning you only if a serious lack of free inodes exists, and only when it's run. Answer D is incorrect because the `tree` command only shows files and directories in a tree-like manner. Answer E is incorrect because the `dumpextfs` command shows many things, but not inode exhaustion or usage.

55. Answer B is correct because only the `du -sh /home` command shows the information needed, with the `-sh` showing a summary in MB/GB of the space usage for the `/home` directory and its contents. Answer A is incorrect because `df -h` shows space usage only on a file system level. Answer C is incorrect because there isn't a `freespace` command on a default Linux machine. Answer D is incorrect because the `dirs` command is for remembering frequently used directories, not showing file usage.

56. Answers A, C, and D are correct because, of the answers listed, they *must* be performed before quotas are enabled for a file system. Answer B is incorrect because it doesn't have to be run to enable quotas but should be run to set users' quota constraints. Answer E is incorrect because the `quota` command is for users to query their disk usage and quota statuses.

57. Answer: `/dev/lp1` (There are no alternative correct answers.)

58. Answer: `/dev/ttyS2` (There are no alternative correct answers.)

59. Answer: `dd if=/dev/hda of=/dev/hdb` (There are no alternative correct answers.)

60. Answers C and D are correct because both can be edited to set the desired result. Answer A is incorrect because there is no such file on a default Linux system. Answer B is incorrect because there is no such file on a default Linux system. Answer E is incorrect because there is no such file on a default Linux system.

61. Answer B is correct because during a user's session the `.xdefaults` file is used to store program customizations. Answer A is incorrect because the `.Xresources` file is only used to load the user's program customizations once when X is started. Answer C is incorrect because `.Xsession` is not related to user customizations. Answer D is incorrect because `xrdb` is the X server resource database utility and has nothing to do with user program customizations.

62. Answer C is correct because the **Files** section is where the FontPath setting is located. Answer A is incorrect because fonts are not a device. Answer B is incorrect because the question is looking for the section and not the keyword for the fonts' location. Answer D is incorrect because there isn't a Display section in the configuration file.

63. Answers A, B, C, D, and E are correct because all are valid X window managers.

64. Answer D is correct because only the **xwininfo** utility shows the current color depth. Answer A is incorrect because **xvidtune** shows the resolution and positioning setting but not the color depth. Answer B is incorrect because **xset** is used to refresh or set parameters in X, not show the color depth. Answer C is incorrect because **xdpyinfo** doesn't show the color depth for the display.

65. Answers A and C are correct because together they are used to configure a customized login screen that can contain graphics and customized welcome text. Answer B is incorrect because the **Xsession** command and **.Xsession** file are used to start the user's session after logging in from *xdm*. Answer D is incorrect because the **XF86Config** file doesn't have any settings that affect a customized login screen for users.

66. Answer B is correct because only the **XF86Config** file is used to set the resolution for X. Answer A is incorrect because the **xinitrc** file is used as a parameter for the **xinit** process and is used to set keymaps and resources, among other settings. Answer C is incorrect because the case is incorrect; it should be **XF86Config-4**. Answer D is incorrect because **serverconfig** isn't a file; it's a directory.

![](img/49f4f38f3aec011238fa50f89e643db3_562_0.png)

# Practice Exam 102

1. Which option to the **modprobe** command causes modules so marked to be removed or unloaded from memory if they haven’t been used for a period of time?   
   - A. autoclean
   - B. inactive
   - C. remove
   - D. timeout
   - E. holdoff

2. Which of the following is not a valid **make** command during a kernel recompile?   
   - A. make dep
   - B. make clean
   - C. make xconfig
   - D. make modules
   - E. make gziplo

3. Which of the following is a valid compilation option for the Linux kernel?   
   - A. make zImage
   - B. make zli1o
   - C. make bzImage
   - D. make li1o

4. You need to load a particular module and all its dependencies with one command. Fill in the blank below with just the command name to accomplish this:
______
