
42: What command will remove an individual Debian GNU/Linux package?

43: What command will upgrade the version of Debian installed?

44: What command will update all available packages from Debian’s update server?

45: If you need a newer version of a package (and still want to use an official Debian package), what distribution version should you look for a new package in?

46: If you need the absolute newest version of a package, than what is provided in Debian stable, what distribution version should you look for the newest package in?

47: What user does Apache run as, in RHEL/CentOS?

## Various Commands & Utilities

48: Which command allows you to view the mail server for an external domain?

49: What command will ‘reverse grep’ a string, showing lines that DON’T match a string?

50: Which command should be used to *append* to a file?

51: Which character (or command) can be used after a command to send the command into the background (while still executing)?

52: What utility allows you to manually test SMTP functionality, troubleshoot firewall restrictions, and connect to other servers?

53: Which command switch to the ‘ping’ utility will allow you to adjust the “TTL, or Time to Live”?

54: What command will allow you to view the routers and hosts that a packet makes its way through, from the computer you are on, to an outside host?

55: What command will show listening network connections, as well as active network connections?

56: What command will allow you to see all processes running on the server?

57: What command will remove an empty directory?

58: What three commands are typically used to compile software, utilizing the standard ‘make’ system?

59: What is the proper syntax to apply a source code patch (called patch.diff) to a source code tree, assuming that the current directory is the root of the source code tree?

60: When compiling the Linux kernel, what is the command to configure the compilation process, using an ncurses-based menu?

61: What is the proper command to use, to delete all compiled executables, and object files from a source directory (most often used to remove these files to troubleshoot compilation issues)?

62: What is the proper command to use, to remove an installed source package, when the source tree used to compile the software is retained (and the current directory is that of the source tree)?

## General Administration

63: What command allows you to change group ownership of a file?

64: If you recently created a new user, but they receive an "access denied" error upon logging onto the server, what command did you forget?

65: What file contains the encrypted password of a user?

66: What file contains most system errors?

67: What command will search for a string, within vi?

68: What command will quit vi, without saving the changes to a file?

69: What single key will allow you to modify a line of text, within vi?

70: What command will write the changes to a file, without quitting vi?

71: What file contains the list of preferred DNS servers to use, when looking up the IP address of a domain name?

72: What file controls text displayed to every user that logs into the server?

73: What file contains a user's shell variable settings, and scripts launched at every login (BASH)?

74: What command will create a shortcut to a file in another directory?

75: What command will create a TAR archive of a directory /home, and store the TAR backup as /backup/backup-home.tar

76: True or false: The 'tar' command will preserve the original permissions on a directory, or file?

77: What command would you use to copy an entire directory (including its contents), to another location?

78: What command will compress the file 'file.tar', using the maximum available compression, and in GZIP format?

## Shells & Shell Scripting

- 79: What file contains a user's shell variable settings, and scripts launched at every login (BASH)?
- 80: What is the most popular shell used today?
- 81: What command will print text that the user running a script can see?
- 82: What line must be included at the beginning of every shell script, in order to ensure that the lines in the script are properly executed?
- 83: What command needs to be executed, if your script gives a "permission denied" error?
- 84: What will the line `DAY=`date \| cut -b 1-4`` do, in a basic shell script?
- 85: What command will send an exit status of 0, in a basic shell script?
- 86: If a script is set to run as the owner of the script, with all the permissions of the script owner, what bit is said to be set on the script?
- 87: What command will set a script to run as the owner of the script, with all of the permissions of that owner?
- 88: What command can be used to make a script pause execution for 5 minutes, then continue script execution?
- 89: What special device will allow all input to be discarded?
- 90: What special device contains truly random characters, and is considered by many to be a replacement to the traditional random device?
- 91: What character is used as a comment designator, in shell scripts?
- 92: What syntax can be used to manually execute a script, that does not have an execute bit set?
- 93: Which single character will allow you to place two separate commands, on a single line?
- 94: Please write the line, which will create an element named "trees", with the separate values 'elm, pine, spruce, fir, dogwood'. This element's values will be used as separate values, and should not be set to a single value.
- 95: Give an example of how to print these separate elements, one per line.

## Firewalls/Routing

96: What device needs to have a value of "1" to enable packet forwarding, between network interfaces?

97: Give an example of an iptables command that will block incoming TCP traffic on port 25, on all network interfaces. This rule should be the last rule in the list, and it should drop the SYN packet that it receives from an external host.

98: Give an example of an iptables command that will block incoming TCP traffic on port 25, when the source address is 209.168.1.8. This rule should be the last rule in the list.

99: Give an example of an iptables command to block all ICMP traffic, on interface eth0. This rule should be the first rule on the list.

100: Give an example of an iptables command that will redirect all traffic on TCP port 25 (eth0) to another host, 192.168.0.5. This rule should be the first rule in the chain.

101: Give an example of an iptables command that will redirect all traffic on TCP port 8080 (eth0) to the host 192.168.0.5, port 80. This rule should be the last rule in the chain.

102: What command will reset all iptables rules to the default policy?

103: Give an example of an iptables command that will block all traffic on TCP port 80 to host 192.168.0.1, with a RST packet. This rule should be the last rule in the chain.

104: Give an example of the syntax used to start a port scan, using the utility NMAP, on the host 192.168.0.10. Pinpointing the host before the scan should be disabled, since the host drops all ICMP traffic.

105: What command will delete the default route?

106: What command will route all external traffic to host 192.168.0.1, via eth0?

107: What command will bring down eth0?

108: What command will bring up eth0?

109: What iptables command should you use to allow traffic on interface eth0, to the SSH service? This command should be the first command in the chain.

110: What iptables command should you use to allow all UDP traffic from host 192.168.0.5? This command should be the first command in the chain.

111: What file controls which hosts are allowed to connect to a Linux server, and is most commonly used by xinetd?

112: What file controls which hosts are not allowed to connect to a Linux server, and is most commonly used by xinetd?

113: Why is it always better to block hosts at the network, or kernel level, rather than at the application level?

114: Which iptables command can be used to enable IP Masquerading, given that eth0 is the inside interface, and that eth1 is the outside interface?

115: What is the iptables command to set the default incoming traffic policy to drop traffic not specifically allowed?
