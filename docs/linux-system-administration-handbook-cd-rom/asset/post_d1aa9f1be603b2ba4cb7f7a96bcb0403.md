
lems says that the computer must not be physically accessible to anyone without access. That is it, it can't be on the network and must be in a locked room to begin with. Chapter 2 has a good list of instructions to keep a typical PC reasonably secure from outside attacks. To quickly sum up:

- Lock the BIOS and set the BIOS to boot only from the C drive.
- Don't use LILO or at least make it boot directly into Linux.
- Don't have DOS or any other OS on the machine.
- Lock the PC case.

You should also have people on hand to assist with problems and prevent anyone from having the chance to take a computer apart.

## 17.2 Software Security

This section is just a bit larger than the hardware security section, and for good reason. With TCP/IP having ever over 65,000 ports available for connecting to a single machine, this gives anywhere up to 65,000 and beyond possible ways for a cracker to enter your system.

### Monitoring Software

Programs like COPS and TripWire allow you to routinely monitor your system to detect possible holes or to detect some forms of break-ins. You should probably get both programs and use them routinely. A program like SATAN will monitor an entire network and report on possible holes. Since many crackers probably have a copy of this, it is probably best to beat them to the punch and run it on your own network before they do.

### Preventing Root Logins

The first way that crackers cause real trouble on your system is by getting root privileges. There are a few ways to do that, and I'll list all of them here, along with suggestions on preventing such things from happening.

First, change the root password often! This way, even if a cracker gets the password, it won't be valid for too long. Also keep an eye on your /etc/security file. This file lists the locations from which root can log in directly. To get root power from any other location, you must first have a valid user account; then use the su command to become root. Root can only log in at the console by default (tty1 through tty8).

Another item that should be done is modifying the su program so only members of the wheel group can su to root. This is a big problem with the Linux su program, in our opinion. The wheel group was designed to be the only group of users that can su into the root account. This limits the number of accounts that can be cracked to get into root. However, the GNU people think this is a bit authoritarian and have their su program designed to allow anyone to su to root, assuming they have the password. Other operating systems, such as SunOS and Solaris, require a user to be in the wheel group before being allowed to su to root.

### Secure Shell (SSH)

You should also start using programs that encrypt passwords as they go over the network. The SSH (secure shell) program is excellent for this, as it not encrypts the password, but also the entire connection. TCP/IP works now, all data are sent over the network in cleartext (i.e., not encrypted). Anyone who has a network sniffer on any machine on the network, or on any network between you and your destination, can read the password you type in. Bad stuff. The SSH program encrypts all this, plus does some checking to verify the host you're connecting from and the host you're connecting to. You should be using this program within your LAN and when connecting to other sites. Commercial versions of SSH for Windows and other platforms are available, allowing all the clients on the network to have secure connections.

The SSH program is designed to be a replacement for the "r-" commands (login, r, rcp) and can install itself so it replaces those commands. If users have .hosts files set up, SSH will still use those files. Users will not have to change their configuration much, but their connections will be more secure.

Setting up SSH requires that you run SSH on the machines you will be talking between. Let's call the client (your personal machine) foo, and the server (where you want to connect, do some administrative work, etc. bar.

> Due to export restrictions and various patents, SSH can't be on the CD-ROM. Go look at the big web search engines for SSH. Read the licensing carefully to make sure you're not breaking any patents or U.S. or local laws in compiling, or having the software.

Bar will run the SSHd (the SSH daemon) which gets started from either the inetd or bootup in daemon mode. If you have a lot of users with SSHd, it might be better to run in daemon mode as SSHd is always ready to make a connection.

The “configure" command sets the stage for compiling and then “make” compiles it. There are few other things you need to do for a typical installation.

The SSHd program runs on the server (bar) and should be started by startup. The client machine (foo) then issues an SSH command similar to login. The command to connect would look something like this:

```
ssh -l foo bar
```

If the bar host is not known to you, you'll get prompted if you want to add it to your list of known hosts. Add the host, and you'll be able to give your password to login.

The global configuration files are located in /etc. These files are /etc/ssh_config for server configuration and /etc/ssh_config for configuration. The options for these files are listed in the man pages for SSH and SSHd.

New hosts can be added to SSH in a global method using the make-SSHknownhosts.

The tcpd program works by following this pattern:

```
daemon_list : client_list [ shell_command ]
```

The daemon list is the name of the program that is running (telnetd, ftpd, and so on). The client list can be any of the following:

- Strings with a. are assumed to be part of a domain (.wayga.net would be any host in the wayga.net).
- Strings ending with a. are assumed to be an IP address net or subnet (128.55.213. would be all the machines that start with that IP address).
- A string starting with @ is assumed to be an NIS netgroup (@hosts all be hosts defined in the NIS netgroup).
- n.n.n/n.m.m.m is a net and mask pair. This gives a bit finer control over the above for matching IP addresses.

There are also a few special keywords:

- ALL—This matches everything.
- LOCAL—All hosts that do not have a dot (.) in the hostname, since local hosts do not typically use the FQDN.
- UNKNOWN—A user whose name is not known (RFC 931 checking) or a host name or IP is unknown.
- KNOWN—Reverse of unknown—a user whose name is known, and both the name and address are known.
- PARANOID—Any host whose reverse DNS does not match the host name's using. Sites with multiple domains may run into this if the reverse DNS and hosts are not synced.

The access control also accepts the word EXCEPT to give something like the following:

```
192.55.242. EXCEPT PARANOID
```
