
## SECURITY

Ensure that your computer BIOS prevents booting from the USB ports, as well as ensure that a system BIOS password is set to prevent other users from changing the boot order.

Along these same lines, anyone who has access to the physical Linux computer could boot the computer and interact with the LILO or GRUB boot loader. This could allow a user to specify options that would boot the system in Single User Mode and gain root access to the system without specifying a password. To prevent this, simply ensure that you set a boot loader password in the LILO or GRUB configuration files, as discussed in Chapter 9.

Another important security consideration for Linux computers is to limit access to graphical desktops and shells. If you leave your workstation for a few minutes and leave yourself logged in to the system, another user can use your computer while you are away. As a result, it is good security practice to lock your desktop environment or exit your command-line shell before leaving the computer. To lock the GNOME or KDE desktop, simply navigate to the Red Hat button and choose Lock Screen; you will need to enter your password to use your desktop again. Exiting a command-line shell also ends any background processes because the parent of those processes is your shell. If you run background processes that take a long time to complete, simply run them using the `nohup command`; this allows you to exit your command-line shell without ending any background processes. For example, to run the `updatedb` command and exit your system afterward such that you can leave your workstation, simply perform the following commands:

```bash
[root@server1 root]# nohup updatedb &
[1] 3773
nohup: appending output to 'nohup.out'
[root@server1 root]# exit

Fedora Core release 2 (Tettnang)
Kernel 2.6.5-1.358 on an i686

server1 login:
```

If you have root access to a Linux system, it is important to minimize the time that you are logged in as the root user to reduce the chance that another user can access your terminal if you accidentally leave your system without locking your desktop or exiting your shell. It is best practice to create a regular user account that you can use to check e-mails and perform other day-to-day tasks. You can then use the `su` [switch user] command to obtain root access only when you need to perform an administrative task. When you are finished, you can use the `exit` command to return to your previous shell where you are logged in as a regular user account, as shown in the following output:

```bash
[user1@server1 user1]$ su - root
Password: ****
[root@server1 root]# _
[root@server1 root]# rm -f /etc/security
[root@server1 root]# exit
[user1@server1 user1] _
```

The `-` option to the `su` command shown in the preceding output loads the root user's environment variables. Also, you can omit the root user's name in the preceding output; if a name is not specified as an argument to the `su` command, the root user is assumed by default.

If you only intend to run one command as the root user, you can instead choose to use the `-c` option to the `su` command; this returns you to your current shell automatically. The following demonstrates how to run the root command shown in the previous output using the `-c` option to the `su` command:

```bash
[user1@server1 user1]$ su -c "rm -f /etc/security" root
Password: *****
[user1@server1 user1]$
```

Still, some users, such as software developers, need to run certain commands as the root user in certain situations. Instead of giving them the root password, it is best to give them the ability to run certain commands as the root user via the **sudo** command. The `sudo` command checks the `/etc/sudoers` file to see if you have rights to run a certain command as a different user. The following `/etc/sudoers` file allows the software developers, `mary` and `bob`, the ability to run the `kill` and `killall` commands as the root user on the computers `server1` and `server2`:

```bash
[root@server1 root]$ cat /etc/sudoers
User_Alias SD = mary, bob
Cmd_Alias KILL = /bin/kill, /usr/bin/killall
Host_Alias SERVERS = server1, server2

SD   SERVERS = (root) KILL
[root@server1 root]$
```

Now, if `mary` needs to kill the `cron` daemon on `server1` (which was started as the root user) to test a program that she wrote, she needs to use the `sudo` command, as shown in the following output, and supply her own password:

```bash
[mary@server1 mary]$ ps -ef | grep crond
root    2281    1    0 21:20 ?    00:00:00 crond
[mary@server1 mary]$ kill -9 2281
-bash: kill: (2281) - Operation not permitted
[mary@server1 mary]$ sudo kill -9 2281

We trust that you have received the usual lecture from the local System Administrator. It usually boils down to these two things:

#1) Respect the privacy of others.
#2) Think before you type.
Password: *****
[mary@server1 mary]$
```

### Protecting Against Network Attacks

Recall from earlier in this chapter that network services listen for network traffic on a certain port number and interact with that traffic. As long as network services exist on a computer, there is always the possibility that crackers can manipulate the network service by interacting with it in unusual ways. One example of this type of network attack is a **buffer overrun**, which can replace program information used by the network service in memory with new program information, consequently altering how the network service operates.

The first step to securing your computer against network attacks such as buffer overruns is to minimize the number of network services running. If you run only the minimum number of network services necessary for your organization, you greatly reduce the chance of network attacks. To see what network services are running on your network, you can run the **nmap** (network mapper) command. The following output demonstrates how `nmap` can be used to determine the number of services running on the `server1` computer:

```bash
[root@server1 root]# nmap -sT server1
Starting nmap 3.5 (http://www.insecure.org/nmap/) at 2005-09-05 9:29 EDT
Interesting ports on server1 (127.0.0.1):
(The 1648 ports scanned but not shown below are in state: closed)

| PORT      | STATE  | SERVICE       |
|:----------|:-------|:--------------|
| 22/tcp    | open   | ssh           |
| 25/tcp    | open   | smtp          |
| 80/tcp    | open   | http          |
| 111/tcp   | open   | rpcbind       |
| 139/tcp   | open   | netbios-ssn   |
| 443/tcp   | open   | https         |
| 445/tcp   | open   | microsoft-ds  |
| 631/tcp   | open   | ipp           |
| 783/tcp   | open   | hp-almgr      |
| 32770/tcp | open   | sometimes-rpc3|
| 32771/tcp | open   | sometimes-rpc5|

Nmap run completed - 1 IP address (1 host up) scanned in 0.928 seconds
[root@server1 root]#
```

From the preceding output, you can determine which services are running on your computer by searching the descriptions for the port numbers in the `/etc/services` file or on the Internet. For services that are not needed, ensure that they are not started automatically by the Internet Super Daemon from entries in the `/etc/rc.d/rc*.d` directories or via lines in other startup scripts such as `/etc/rc.d/rc.local`.

For services that must be used because they are essential to your organization, you can take certain steps to ensure that they are as secure as possible. For example, you could enable encryption for network services that support encrypted communication (for example, `sshd`), and use netfilter/iptables INPUT chain rules to allow only desired network traffic to reach your network services. It is also important to ensure that network service daemons are not run as the root user on the system when possible. If a cracker gains access to your system via a network service daemon run as the root user, the cracker has root access as well. Many network daemons, such as Apache, set the user account by which they execute in their configuration files.

In addition, because network attacks are reported in the open source community, new versions of network services usually include fixes for known network attacks. As such, these new versions are more resilient to network attacks. Because of this, it is good form to periodically check for new versions of network services, install them, and check the associated documentation for new security-related parameters that can be set in the configuration file.

If you use network services that are started by the Internet Super Daemon, you can use TCP wrappers to provide extra security. A **TCP wrapper** is a program (`/usr/sbin/tcpd`) that can start a network service. To enable TCP wrappers, you must modify the appropriate file in the `/etc/xinetd.d` directory and start the network daemon as an argument to the TCP wrapper. For the telnet daemon, you modify the `/etc/xinetd.d/telnet` file, as shown in the following example:

```bash
[root@server1 root]# cat /etc/xinetd.d/telnet
# default: on
# description: The telnet server serves telnet sessions; it uses \n#
uncrypted username/password pairs for authentication.

service telnet
{
    flags            = REUSE
    socket_type    = stream
    wait           = no
    user           = root
    server         = /usr/sbin/tcpd
    server_args    = /usr/sbin/in.telnetd
    log_on_failure += USERID
    disable        = yes
}
[root@server1 root]# _
```

Now, the telnet daemon (`/usr/sbin/in.telnetd`) will be started by the TCP wrapper (`/usr/sbin/tcpd`). Before a TCP wrapper starts a network daemon, it first checks the `/etc/hosts.allow` and `/etc/hosts.deny` files. This allows you to restrict the network service such that it can only be accessed by certain hosts within your organization. The following `/etc/hosts.allow` and `/etc/hosts.deny` files only allow the computers `client1` and `client2` the ability to use the telnet utility to connect to your telnet server.

```bash
[root@server1 root]# cat /etc/hosts.deny
in.telnetd: ALL
[root@server1 root]# _
```
