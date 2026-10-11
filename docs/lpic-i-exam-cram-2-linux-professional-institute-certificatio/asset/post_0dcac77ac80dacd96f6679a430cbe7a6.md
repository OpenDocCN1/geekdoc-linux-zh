
## 34. Answer: `~/.bashrc` (An alternative answer is `$HOME/.bashrc`.)

## 35. Answers A and C are correct because they have a lock function, which is what caused the `L` in front of the encrypted password. Answer B is incorrect because `chfn` is used to change the `finger`-related information for users. Answer D is incorrect because `chattr` is used for changing the file attributes viewable by `lsattr`. Answer E is incorrect because `chpasswd` is used for setting users' passwords in batches or bulk mode.

## 36. Answer: `atq` (There are no alternative correct answers.)

## 37. Answer: `groups snuffy` (There are no alternative correct answers.)

## 38. Answer: `/etc/syslog.conf` (There are no alternative correct answers.)

## 39. Answer: `mesg n` (There are no alternative correct answers.)

## 40. Answers B and C are correct because you must be running X and must start the `xconsole` application to show the messages being directed to the configured target. Answer A is incorrect because `/dev/xconsole` is a pipe, not a program. Answer D is incorrect because Xconsole isn't the name of the application, nor must you run it in the background with an `&` character. Answer E is incorrect because you must be in X and must start the `xconsole` application to see these messages.

## 41. Answer B is correct because all authentication messages are sent to the `auth` facility. Answer A is incorrect because there isn't a login facility. Answer C is incorrect because authentication messages for users are still sent to the `auth` facility. Answer D is incorrect because the `daemon` facility is a miscellaneous or catch-all facility for daemons that don't have a particular category. Answer E is incorrect because there isn't a secure facility.

## 42. Answer E is correct because it most simply accomplishes sending all but `debug` to the target because `debug` is not included by default. Answer A is incorrect because `debug` is never shown unless specifically requested. Answer B is incorrect because it sends only the `info` priority messages, not `info` and higher. Answer C is incorrect because it's not the simplest method to show all but `debug` messages, although it will work. Answer D is incorrect because it sends `debug` and higher priority messages.

## 43. Answer B is correct because the keyword `server` is prefixed before time sources in the `/etc/ntp.conf` file. Answer A is incorrect because `source` is what is being configured, but the keyword is `server`. Answer C is incorrect because `tier1` is a description of a type of server, not a keyword. Answer D is incorrect because `fudge` is a keyword that prefixes a fake server used for backup synchronization. Answer E is incorrect because you must prefix the server's address with the keyword `server`.

## 44. Answer D is correct because it alone can be used to configure the IP address information needed for NICs. Answer A is incorrect because it shows connections and socket information but can't change IP settings. Answer B is incorrect because it's the wireless configuration utility that's part of some distributions, but none of the NICs are specified as wireless. Answer C is incorrect because there isn't a command named default. Answer E is incorrect because the route command is only capable of showing or managing the routing and gateway information for a system, not setting the IP settings.

## 45. Answer C is correct because your nephew forgot to put a 1 in the /proc/sys/net/ipv4/ip_forward file so the system will forward traffic between the interfaces. Answer A is incorrect because it uses the set command and attempts to set a 1 to a nonexistant file. Answer B is incorrect because it has no affect on routing. Answer D is incorrect because echo'ing a 1 into a file isn't possible and a > redirect symbol should be used.

## 46. Answer C is correct because the use of -n with traceroute keeps the names from being resolved and just prints the IPs of routers it finds, speeding things up measurably. All other answers are incorrect because they don't produce the desired result.

## 47. Answer B is correct because the minicom application is a quick and easy method to determine whether connectivity is present for a Linux dial-up connection. Answer A is incorrect because setserial is used beforehand to set up the serial port used by a dial-up connection. Answer C is incorrect because it's a Windows application that does much the same thing as minicom. Answer D is incorrect because it's an older DOS application that was used for modem communications.

## 48. Answers A, B, and C are correct because they are specified in the RFC as private address ranges. Answer D is incorrect because it's a network that was often used in the early days of training for IP subnetting classes, even though it's a publicly addressable range of addresses.

## 49. Answers C and D are correct because you want named to run standalone for speed, but to configure the /etc/hosts.deny file to block the undesirable networks from attacking the server. Answer A is incorrect because running named under xinetd slows it down, mostly when it has to be started on demand. Answer B is incorrect because using tcpd introduces a layer of complexity and slows down named. Answer E is incorrect because you are denying particular networks of hosts, so the specific configuration should be in the /etc/hosts.deny file.

## 50. Answer E is correct because the **holdoff** timer option causes the connection to be delayed in reconnecting to give the other end time to reset. Answer A is incorrect because the waitone timer option doesn't exist. Answer B is incorrect because restart isn't a valid option for a connection. Answer C is incorrect because disable is not a valid option in this case. Answer D is incorrect because **connect-delay** is used only when a connection has been gracefully completed, not broken or interrupted.

## 51. Answers A, C, and E are correct because they are routing daemons or engines on a Linux system. Answer B is incorrect because the *route* command is simply a command, not a daemon or an engine. Answer D is incorrect because **rtnetlink** is a description of a routing socket, not a daemon or an engine.

## 52. Answer C is correct because the **/etc/services** file lists the services and their associated ports for the machine. Misconfiguring this file disables services. Answer A is incorrect because an **/etc/sysnconf/scripts** file doesn't exist on Linux. Answer B is incorrect because the **/etc/resolv.conf** file is for name resolution, not services and their ports. Answer D is incorrect because it's referring to the **c:\windows\system32\drivers\etc\services** file on a Windows system.

## 53. Answer: **route add 172.16.38.125 lo** (An alternative answer is **route add 172.16.38.125 gw 127.0.0.1**.)

## 54. Answer: **route add default gw 10.1.2.3** (There are no alternative correct answers.)

## 55. Answer A is correct because only the **dig** command with the **example.com** domain and the **mx** specifier show the requested records. Answer B is incorrect because the **host** command doesn't show specific servers in a domain; it shows just the resolved IP for the name queried. Answer C is incorrect because the **nslookup** command doesn't query for the **mx** record as shown and requires more options. Answer D is incorrect because the **traceroute** command doesn't have a --**mnail** option.

## 56. Answer: **/etc/exports** (There are no alternative correct answers.)

## 57. Answers B and E are correct because they are the two components of the Samba suite, which masquerades a Linux/Unix system as a Windows server for file and printer sharing. Answer A is incorrect because NFS usage for Windows client systems requires extra software and configuration. Answer C is incorrect because Tarantella is a commercial software package and requires a license. Answer D is incorrect because the **wu-ftpd** daemon is for FTP and doesn't affect printer sharing.

## 58. Answer B is correct because the `/etc/exports` file can be edited to contain just the characters `/shared` to make the files available to all hosts read-only via NFS. Answer A is incorrect because this is the file that should be edited on a Solaris box to share these files. Answer C is incorrect because this file doesn't exist on a Linux box by default. Answer D is incorrect because this file doesn't exist on a Linux box by default. Answer E is incorrect because this file doesn't exist on a Linux box by default.

## 59. Answer D is correct because the DocumentRoot is the directive that sets the path for the content on the system. All other answers are incorrect because they are not directives in the Apache configuration file.

## 60. Answer C is correct because only the `apachectl` command gracefully (without aborting current sessions) restarts the `httpd` process. All other answers destructively restart the `httpd` process, severing current connections.

## 61. Answer: `newaliases` (There are no alternative correct answers.)

## 62. Answer: `mailq` (An alternative answer is `sendmail -bp`.)

## 63. Answer: `/var/spool/mail` (There are no alternative correct answers.)

## 64. Answer B is correct because a subnet mask of 224 means 3 bits are taken for the network, which exactly matches the requirement for six subnets. Answer A is incorrect because it allows for only two subnets. Answer C is incorrect because it doesn't custom subnet the network at all, allowing only a single network. Answer D is incorrect because it allows for more than six networks but means that instead of 30 hosts per subnet, only 14 hosts are possible per subnet. Answer E is incorrect because it allows for only six hosts per subnet.

## 65. Answer: `testparm` (There are no alternative correct answers.)

## 66. Answer: `scp -r` (There are no alternative correct answers.)

## 67. Answer: `netbios name = boomer` (An alternative answer is `netbios name=boomer`.)

## 68. Answer D is correct because the `chkconfig` command is used to manage the services in both the runlevels and those controlled by `xinetd/inetd`, and running that command turns on or sets `disallow = no` for the Telnet service. Answer A is incorrect because the `chkconfig` command shown doesn't modify the `runlevel` directory entries. Answer B is incorrect because the `services` file doesn't contain yes and no parameters. Answer C is incorrect because `chkconfig` doesn't affect the lines or entries in `rc.sysinit`.
