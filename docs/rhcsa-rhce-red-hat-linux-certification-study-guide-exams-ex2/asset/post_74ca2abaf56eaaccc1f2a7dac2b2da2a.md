
install the ntp package. Without that package, the chkconfig ntpd on command would lead to an error message.

Sometimes, there are mutually exclusive alternatives. For example, for SMTP services, RHEL 6 makes it possible to configure either Postfix or sendmail. In Chapter 13, you'll examine a different way to make sure only one service is set to run.

Of course, it is always possible that during an exam, you'll be told to make sure a service does not start during the boot process. And in a production environment, the installation of so many services on a single system is rare, because of the security risks.

## Review Access Through Layers of Security

The first place to check a service is from the local system. For example, if you can connect to an FTP server from that system, that confirms a good configuration of that service. Some issues relate to SELinux; others relate to various user and host-based firewalls. For issues beyond SELinux, the network command tools installed in Chapter 2 can be quite helpful.

## Troubleshoot SELinux Issues

If the configuration is good but still does not work, that suggests an SELinux issue. Not all SELinux issues are readily visible. However, you can check two basic issues with respect to SELinux:

- The list of boolean settings related to the configuration option in question. For example, users who try to connect to remote home directories through the FTP server can be configured through the main vsFTP configuration file. However, problems don't always appear in the SELinux logs.
- The SELinux file contexts. The contexts of the target directories should match those of default directories. In other words, when you run the ls -Z command on a shared FTP directory, the file contexts should match that of the default shared FTP directory.

The next step is to test the connection from a remote system. It's appropriate to test the connection in a number of ways:

- 1. Can the remote client system communicate with the remote server? That's most easily confirmed with the ping command.
- 2. Can the remote client communicate over the assigned port? That can be confirmed with the telnet command. For example, the following command attempts to establish a connection on TCP/IP port 21:

```
$ telnet 192.168.122.50 21
```

If the connection is successful, the vsFTP server is identified by name. Type in the quit command and press ENTER to exit from the connection.
- 3. If the telnet connection to the appropriate port does not work, then there may be a firewall problem. There are actually subtle differences
  - a. Firewalls exist on several levels. The iptables command firewall discussed in Chapters 4 and 10, as configured in /etc/sysconfig/iptables, must support access through the noted port number and can't limit it from desired hosts.
  - b. The TCP Wrappers system works with daemons associated with the libwrap.so.0 library, allowing and limiting access in /etc/hosts.allow and /etc/hosts.deny.

If all firewalls are clear, and the service still does not work as intended, then there may be a configuration problem with the server. Some servers include their own limits, based on hosts, IP addresses, and user names.

## Troubleshoot iptables-Based Firewall Issues

In general, iptables-based firewalls are straightforward. If a system allows access for server communications, you'll see it in the port numbers documented in the /etc/sysconfig/iptables file and the output to the iptables -L command.
Specifically, you should expect to see a line like the following in /etc/sysconfig/iptables to allow communications through the standard port for the SSH server:

```
-A INPUT -m state --state NEW -m tcp -p tcp --dport 22 -j ACCEPT
```

When the iptables service is started with the /etc/init.d/iptables start command, the file is read into memory; you should be able to see the following excerpt from the iptables -L command for the noted port:

```
ACCEPT tcp -- anywhere anywhere state NEW tcp dpt:ssh
```

Let's translate that line into something closer to English. This rule accepts packets. It checks the packet for the use of the TCP protocol. It then checks the IP addresses of the header but allows packets that come from any address, with a destination of
any address. The packet is new, with a TCP destination port (dpt) associated with ssh. The /etc/services file translates ssh to the standard SSH port of 22.

Of course, you could just use the Firewall Configuration tool described in Chapters 4 and 10, but what if those tools are flawed? The bottom line for iptables-based firewalls is based on the noted file and the way it's implemented with the iptables -L command.

Unless this port is open in the firewall, an attempt to connect to that server is rejected with a message like the following:

```
ssh: connect to host server1.example.com port 22: No route to host
```

In contrast, the telnet server1.example.com 22 command leads to a similar message:

```
telnet: connect to address 192.168.122.50: No route to host
```

## Troubleshoot TCP Wrappers Firewall Issues

In contrast, if the service is protected by TCP wrappers, the error message behavior is different. For this section, I configured the /etc/hosts.allow and /etc/hosts.deny files on the server1.example.com system to allow access only from .example.com systems on the 192.168.122.0/24 network. That means access is not allowed from systems such as outsider1.example.org on IP address 192.168.100.100.

In that case, when I tried accessing the server1.example.com system with the ssh command, I received the following error message:

```
ssh_exchange_identification: Connection closed by remote host
```

In contrast, the telnet server1.example.com 22 command from the same system returns the following messages, which stops for a moment:

```
Trying 192.168.122.50
Connected to server1.example.com.
Escape character is '^]'
```

For a few moments, it appears the system is about to connect. But then the block from TCP Wrappers results in the following message:

```
Connection closed by foreign host.
```

## EXERCISE 11-2

### Review the Different Effects of iptables and TCP Wrappers

This exercise assumes an operational vsFTP server, similar to the one configured in Chapter 1 for installations. It is assumed that you'll configure that vsFTP server on the server1.example.com system. You'll then make sure the firewall blocks traffic on the standard vsFTP port, 21, before checking the effect from a remote blocked system, outsider1.example.org. To review, these systems as configured in Chapters 1 and 2 are on IP addresses 192.168.122.50 and 192.168.100.100, respectively.

Then you'll open up the firewall on port 21 and then limit access using TCP Wrappers. There are a lot of steps in this exercise; in fact, each numbered step requires several commands or actions. In some cases, the required command is implied. For example, since there are two versions of the Firewall Configuration tool, the exact steps required would differ.

- 1. If it is not already installed, install the vsFTP server, as discussed in the chapter. Make sure that server is active with the `/etc/init.d/vsftpd start` command.
- 2. Start the Firewall Management tool with the `system-config-firewall` command. Make sure FTP is not activated in the list of Trusted Services. Make sure the changes are applied and then exit from the Firewall Management tool.
- 3. Try connecting to the vsFTP server from the local system with a command like `lftp localhost`. It should work, which you can confirm from the `lftp localhost:/>` prompt with the `ls` command. Exit from the vsFTP server with the `quit` command.
- 4. Move to the outsider1.example.org system. It's acceptable to connect to it via SSH; in fact, that may be the only method available to connect to that system on an exam (and in real life).
- 5. Try pinging the system with the vsFTP server with the `ping 192.168.122.50` command. Remember to press `CTRL-C` to stop the process. Try connecting to the vsFTP server with the `lftp 192.168.122.50` command. What happens? Try to connect to the system with the `telnet 192.168.122.50 21` command. What happens?
- 6. Return to the server1.example.com system. Open the Firewall Configuration tool again, and this time, make FTP a trusted service. Don't forget to apply the change, before exiting from the Firewall Configuration tool.
