
of bytes received by the kernel but not read by the process. Next, the Send-Q column tells us the number of bytes sent to the other side of the connection but not acknowledged.

The fourth, and sixth columns are the most interesting in terms of system security. The Local Address column tells you your own server's IP address and port number. Remember that your server recognizes itself as 127.0.0.1 and 0.0.0.0 as well as its normal IP address. In the case of multiple interfaces, each port being listened to will show up on both interfaces and thus as two separate IP addresses. The port number is separated from the IP address by a colon. In the output from the netstat example shown above, one Ethernet device has the IP address 192.168.1.1, and the PPP connection has the address 209.179.251.53. Your IP addresses will vary depending on your setup.

The fifth column, Foreign Address, identifies the other side of the connection. In the case of a port that is being listened to for new connections, the default value will be 0.0.0.0:*. This IP address means nothing since we're still waiting for a remote host to connect to us!

The sixth column tells us the State of the connection. The man page for netstat lists all of the states, but the two you'll see most often are LISTEN and ESTABLISHED. The LISTEN state means there is a process on your server listening for the port and ready to accept new connections. The ESTABLISHED state means just that—a connection is established between a client and server.

## Security Implications of netstat's Output

By listing all of the available connections, you can get a snapshot of what the system is doing. You should be able to explain and justify all ports listed. If your system is listening to a port that you cannot explain, this should raise suspicions.

If you've been using your memory shell for other purposes and haven't memorized the services and their associated port numbers, you can look up the matching info you need in the /etc/services file. Some services, however (most notably those that use the portmapper), don't have set port numbers but are valid services. To see which process is associated with a port, use the -p option with netstat. On the lookout for odd or unusual processes using the network. For example, if the BASH shell is listening to a network port, you can be fairly certain that something odd is going on.

Finally, remember that you are only interested in the destination part of a connection; this tells you which service is being connected to and whether it is legitimate. Unfortunately, netstat doesn't explicitly tell us who originated a connection, but with a little thinking we can usually figure it out. The general rule of thumb is that the side whose port number is greater than 1024 is the side that originated the connection. Obviously, this general rule doesn't apply to services typically running on ports higher than 1024, such as X Windows (port 6000).

## Shutting Down Services

One purpose for the netstat command is to determine what services are enabled on your servers. Making Linux easier to install and manage right out of the box has led to more and more default settings that are unsafe, so keeping track of services is especially important.

When you’re evaluating which services should stay and which should go, answer the following questions:

- **Do we need the service?** The answer to this question is very important. In most situations, you should be able to disable a great number of services that start up by default. A stand-alone Web server, for example, should not need to run NFS.
- **If we do need the service, is the default setting secure?** This question can also help you eliminate some services—if they aren’t secure and they can’t be made secure, then chances are they should be removed. The Telnet service, for instance, is often a candidate for early removal because it requires that passwords be sent over the Internet without encryption.
- **Does the service software need updates?** All software needs updates from time to time, such as that on Web and FTP servers. This is because as features get added, new security problems crop in. So be sure to remember to track the server software’s development and get upgrades installed as soon as security bulletins are posted.

### Shutting Down inetd Services

To shut down a service that is started via the *inetd* program, simply edit the *file/inetd.conf* configuration file and comment out the service. To designate the service entry as a comment, start the line with a number sign (#). See Chapter 9 for more information on the inetd. Remember to send the HUP signal to *inetd* once you’ve made any changes to the *file/inetd.conf* file. Type the following command:

```bash
[root@localhost /root]# /etc/init.d/inetd reload
```

### Shutting Down Non-inetd Services

If a service is not run by *inetd*, then it is being run by a process that is probably started at *boot* time. The easiest way to stop that from happening is to change the *script*. Go to the *file/etc/rc.d* directory and find the symbolic links that point to the startup script. In one of the `rc` directories, (see Chapter 7 for information on startup scripts), I rename the symbolic link to start with X instead of S. Should you decide to restart a service, it’s easy to rename it again starting with an S. If you have renamed the startup script but want to *stop* the currently running process, use the *ps* command to find the process ID number and then the *kill* command to actually terminate the process. For example, here are the commands to kill a *portmap* process, and the resulting output:

```bash
[root@localhost /root]# ps aux | grep portmap
bin 255 0.0 0.1 1084 364 ? S 0u308 0:00 portmap
root 6834 0.0 0.1 1352 440 pts/0 S 01:55 0:00 grep portmap
[root@localhost /root]# kill 255
```

> NOTE: As always, be sure of what you’re killing before you kill it, especially on a production server.

## A Note About the syslog Service

One non-inited service that will pop up on *netstat* output but can be safely ignored is *syslog*. This service has historically defaulted to binding to a network port and listening for network messages to log. Because of the danger of lodging arbitrary messages from a network, Linux developers have added a mechanism whereby *syslog* only logs requests sent from other hosts if it has been started with the *-r* option. By default, *syslog* does not start with *-r*, so you can safely let it remain on your system.

## MONITORING YOUR SYSTEM

The process of tying down your server's security isn't just for the sake of securing your server, but it is also to give you the opportunity to clearly see what normal server behavior should look like. After all, once you know what normal behavior is, unusual behavior will stick out like a sore thumb (e.g., if you turned off your talent scanner when setting up the server, seeing a log entry for talent means something is very wrong!).

Commercial packages that perform monitoring do exist and may be worth checking out for your site as a whole, but we'll leave the discussions of their capabilities to *Network World* or *PC Week*. Here, we'll take a look at a variety of other excellent tools that help you accomplish the monitoring of your system. Some of these tools come with all Linux distributions; some don't. All are free and easily acquired.

## Making the Best Use of syslog

In Chapter 9 we explored *syslog*, the system logger that saves messages from various programs into a set of text files for record-keeping purposes. By now, you've probably seen the type of log messages we get with *syslog*. These include security-related messages such as who has logged into the system, when they logged in, and so forth.

As you can imagine, it's possible to analyze these logs to build a time-lapse image of the utilization of your system services. This data can also point out questionable activity.

For example, why was the host *crackerpoisonothing-better-to-do.net* sending so many Web requests in such a short period of time? What was he looking for? Has he found a hole in the system?

## Log Parsing

Doing periodic checks on the system's log files is an important part of maintaining security. Unfortunately, scrolling through an entire day's worth of logs is a time-consuming and unerringly boring task that reveals few meaningful events. To ease the drudgery, pick up a text on scripting language (such as Perl) and write small scripts to parse out the logs. A well-designed script works by throwing away what it recognizes as normal behavior and showing everything else. This can reduce thousands of log entries for a day's worth of activities down to a manageable few lines. This is an effective way to detect attempted break-ins and possible security gaps. Hopefully, it'll become entertaining to watch the script kiddies trying and failing to break down your walls.
