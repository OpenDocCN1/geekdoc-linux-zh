
xinetd access_times option is set to 8:00–17:00 and somebody logs in at 4:59 p.m. (one minute before the end time), that user may continue using the system well beyond the 5:00 p.m. cutoff time.

You should enter these options into the files in /etc/xinetd.d that correspond to the servers you want to protect. Place the lines between the opening brace (`{`) and closing brace (`}`) for the service. If you want to restrict all your xinetd-controlled servers, you can place the entries in the default section in /etc/xinetd.conf.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_541_0.png)

Some servers provide access control mechanisms similar to those of TCP Wrappers or xinetd. For instance, Samba provides hosts allow and hosts deny options that work much like the TCP Wrappers file entries.

These options are most common on servers that are awkward or impossible to run via inetd or xinetd.

## Configuring a Firewall

Although the Linux+ exam objectives don't mention firewalls, you should be familiar with the concept. A firewall is a computer that restricts access to other computers or software that runs on a single computer to protect it alone. Broadly speaking, two types of firewalls exist: packet-filter firewalls, which work by blocking or permitting access based on low-level information in individual data packets (such as source and destination IP addresses and ports), and proxy filters, which partially process a transaction (such as a Web page retrieval) and block or deny access based on high-level features in this transaction (such as the filename of an image in the Web page).

In Linux, the kernel includes packet-filter firewall capabilities, which can be programmed via the iptables program. You can set up rules by typing iptables followed by various options that define specific restrictions, such as limits on the IP addresses that may access a specific network port. Creating an effective firewall requires learning iptables in detail and writing a script that calls this program repeatedly to set up specific rules.

Many distributions make things easier by providing a generic firewall script that you can configure using a GUI tool. These tools are generally designed for protecting a single computer against unwanted outside access. Check your distribution's GUI system administration options for a firewall configuration tool. You may be able to set security based on a few levels (high, medium, and low security, for instance) or in a somewhat more refined manner.

Linux can also function as a firewall computer that protects an entire network; however, such a configuration is likely to require in-depth knowledge of iptables, as well as topics such as configuring Linux as a router.

## Disabling Unused Servers

Quite a few server programs ship with most Linux distributions, which can be a great advantage—you don't need to hunt for servers you want to run. On the other hand, this very advantage can be a drawback—if you're not careful, you can end up running a server and not even realize it's installed! For this reason, you should periodically search for servers and shut down any that you find that aren't really necessary. You must begin this task by locating unwanted servers. Several tools to do so exist, such as `netstat`, `lsof`, and remote network scanners. You can also search your local configuration files for clues about what may be running. Disabling unused servers can be done by uninstalling the package or by reconfiguring the server.

## Using netstat

One way to begin diagnosing network security is to look for network activity or open ports on a computer. One tool that can help in this respect is **netstat**. This program is the Swiss Army knife of network status tools; it provides many different options and output formats to deliver information about routing tables, interface statistics, and so on. For spotting unnecessary servers, you can use netstat with its `-a` and `-p` options, as shown here:

```
# netstat -ap
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address                 Foreign Address               State
PID/Program name
tcp        0      0 *:ftp                 *:*                   LISTEN
690/inetd
tcp        0      0 tee1a.rodsbooks.com:ssh nessus.rodsbooks.com:39361 ESTABLISHED
787/sshd
```

![](img/f339a9f48c4b443e61c74acb4c9c3da4_542_0.png)

I've trimmed most of the entries from this output to make it manageable as an example. Also, `netstat` can be run as an ordinary user, but it may not return as much information. Specifically, only root and a process's owner see the PID and program name of a process.

This version of the `netstat` command shows active network connections, which can reveal the presence of servers that are running on your computer. The Local Address and Foreign Address columns specify the local and remote addresses, including both the host-name or IP address and the port number or associated name from `/etc/services`. The first of the two entries shown here isn't actively connected, so the local address, the foreign address, and the port number are all listed as asterisks (*). This entry does specify the local port, though: *ftp*. This line indicates that a server is running on the ftp port (TCP port 21). The State column specifies that the server is listening for a connection. The final column in this output, under the PID/Program name heading, indicates that the process with a process ID (PID) of 690 is using this port. In this case, it's inetd. In other words, this server is running and listening for connections, but nobody is currently connected to it.

The second output line indicates that a connection has been established between tee1a.rodsbooks.com and nessus.rodsbooks.com (the second hostname is truncated). The local system (tee1a) is using the ssh port (TCP port 22), and the client (nessus) is using port 39361 on the client system. The process that's handling this connection on the local system is sshd, running as PID 787.

It may take some time to peruse the output of netstat, but doing so will leave you with a much improved understanding of your system's network connections. If you spot servers listening for connections that you didn't realize were active, you should investigate the matter further. Some servers may be innocent or even necessary. Others may be pointless security risks.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_543_0.png)

> When you use the -p option to obtain the name and PID of the process using a port, the netstat output is wider than 80 columns. You may want to open an extra-wide xterm window to handle this output or redirect it to a file that you can study in a text editor capable of displaying more than 80 columns. To quickly spot servers listening for connections, type netstat -lp rather than netstat -ap. The result will show all servers that are listening for connections, omitting client connections and specific server instances that are already connected to clients.

Exercise 10.1 demonstrates the use of netstat to monitor network port use.

## EXERCISE 10.1

### Monitor Network Port Use

To get started with netstat, follow these steps:

- Log into the Linux system as a normal user. (Acquiring root privileges will produce more complete output, as described earlier, but isn't strictly necessary for this exercise.)
- Launch an xterm from the desktop environment's menu system, if you used a GUI login method.
- Type `netstat -ap | less`, and page through the output. Chances are, you'll see quite a few entries for servers that are listening for connections and for established connections to local servers or from local clients to remote servers. Pay particular attention to servers that are listening for new connections—that is, those that list LISTEN in the State column of the output.
- Type `netstat -ap | grep ssh` to find connections involving SSH. Depending on your configuration and the servers you have running, you may see no output or many lines of output.
