58. Answer B is correct because the `/etc/exports` file can be edited to contain just the characters `/shared` to make the files available to all hosts read-only via NFS. Answer A is incorrect because this is the file that should be edited on a Solaris box to share these files. Answer C is incorrect because this file doesn't exist on a Linux box by default. Answer D is incorrect because this file doesn't exist on a Linux box by default. Answer E is incorrect because this file doesn't exist on a Linux box by default.

59. Answer D is correct because the DocumentRoot is the directive that sets the path for the content on the system. All other answers are incorrect because they are not directives in the Apache configuration file.

60. Answer C is correct because only the `apachectl` command gracefully (without aborting current sessions) restarts the `httpd` process. All other answers destructively restart the `httpd` process, severing current connections.

61. Answer: `newaliases` (There are no alternative correct answers.)

62. Answer: `mailq` (An alternative answer is `sendmail -bp`.)

63. Answer: `/var/spool/mail` (There are no alternative correct answers.)

64. Answer B is correct because a subnet mask of 224 means 3 bits are taken for the network, which exactly matches the requirement for six subnets. Answer A is incorrect because it allows for only two subnets. Answer C is incorrect because it doesn't custom subnet the network at all, allowing only a single network. Answer D is incorrect because it allows for more than six networks but means that instead of 30 hosts per subnet, only 14 hosts are possible per subnet. Answer E is incorrect because it allows for only six hosts per subnet.

65. Answer: `testparm` (There are no alternative correct answers.)

66. Answer: `scp -r` (There are no alternative correct answers.)

67. Answer: `netbios name = boomer` (An alternative answer is `netbios name=boomer`.)

68. Answer D is correct because the `chkconfig` command is used to manage the services in both the runlevels and those controlled by `xinetd/inetd`, and running that command turns on or sets `disallow = no` for the Telnet service. Answer A is incorrect because the `chkconfig` command shown doesn't modify the `runlevel` directory entries. Answer B is incorrect because the `services` file doesn't contain yes and no parameters. Answer C is incorrect because `chkconfig` doesn't affect the lines or entries in `rc.sysinit`.