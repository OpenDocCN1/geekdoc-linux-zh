# CHAPTER 12 Network Configuration 333

with these utilities, we will focus on using these command-line utilities to manipulate network settings in this section.

# ifconfig

ifconfig program is one of several available mechanisms for setting up NICs. All of its operations can be performed through command-line options, as its native format has no menus or graphical interface. Even though it is popular, the use of ifconfig is slowly becoming deprecated by some Linux distributions, and people are encouraged to use the tools that ship with the iproute package (for example, ip).

Administrators who have used the Windows ifconfig program may see some similarities, as Microsoft implemented some CLI networking tools to mimic functional subsets of their UNIX counterparts.

> NOTE ifconfig program typically resides under the /sbin or /usr/sbin/ directory, which is included in root's PATH.
Some login scripts, such as in openSUSE, do not include /sbin or /usr/sbin/ in the PATH for unprivileged users by default. You, might need to find the full path to the command, like /sbin/ifconfig or /usr/sbin/ifconfig, when calling it as a regular user. If you expect to be a frequent user of commands or under /sbin, you might find it to add /sbin or /usr/sbin/ to your PATH.

> TIP Administrators managing Windows servers may find the %SYSTEMROOT%\system32\netsh.exe a program tool for exposing and manipulating the details of Windows networking via the CLI.

# ip

Another powerful program that can be used to manage network devices in Linux is the ip program. The ip utility uses the iproute and iproute2 software packages. The package containing networking utilities (such as ip) are designed to be used to take advantage of and manipulate the advanced networking capabilities of the Linux kernel. The syntax for the ip utility is a little terse and less forgiving than that of the ifconfig utility. But the ip is much more powerful.

# nmcli

The newest kid on the block when it comes to managing network devices and connections in the Linux world is the suite of tools that comes with the NetworkManager package. One of such is the command-line nmcli utility, which can be used to control the NetworkManager daemon.

One distinguishing concept in the NetworkManager world is the notion of connections (or profiles). A connection or profile is a collection of related information that describes how to create or connect to a network. NetworkManager stores all network configuration (MAC addresses, IP addresses, DNS, gateways, and so on)