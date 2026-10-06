
# 170 Part II ✦ SUSE System

## Listing 6-1: Output of route -n

```
bible:usr/sbin # route -n
Kernel IP routing table
Destination    Gateway      Genmask Flags Metric Ref Use Iface
192.168.131.0   0.0.0.0     255.255.255.0 U      0   0      eth0
169.254.0.0     0.0.0.0     255.255.255.0 U      0   0      eth0
127.0.0.1       0.0.0.0     255.0.0.0   U      0   0      lo
192.168.131.254 0.0.0.0     255.255.255.0 UG     0   0      eth0
```

In this example, the IP address of the machine called bible is 192.168.131.70/255.255.255.0. As you can see from the routing table, there is a route to the 192.168.131.0 network through the eth0 device.

The 0.0.0.0 IP address we talked about before can be in the code output, and this refers to the default route we are using if our routing table does not understand to communicate with a machine we specify.

In this case, the default route is 192.168.131.254. This is the IP address of a router connects to the Internet.

When a packet is received by your router, it will roughly do the same thing with your TCP/IP packet, distinguishing it knows how to send the packet directly to a network it is connected to or whether it should send the packet to a preferred route.

Depending on what capabilities the router has and where the router is on the Internet, it may know the best route for the network you are trying to communicate with directly. This usually happens only on larger core routers, but this is how a packet eventually ends up at its destination. Larger routers know where to send a packet because they have more connections to core parts of the Internet. This kind of router is usually your ISP's router, which has a link to the backbone Internet connection of a country or region.

# Breathe...

TCP/IP is not an easy technology to comprehend, but you should now have enough information to understand the basics of TCP/IP and how it relates to Linux throughout the rest of the book.

## Logging

Linux books provide separate chapters on logging, discussing log files only in the context of the applications that create them. In reality, Linux stores all of the log files for system applications in a single directory, examining logging as a general concept provides some insights, should you ever need to try to diagnose a system problem on your system.

Logging is the way that Linux tells you what is happening, from general status information to error logging. This proves very useful for day-to-day diagnostics and should be the first port of call for any anomalies that you find on your system.

We will talk about the de facto logging facility in Linux, syslog; the newer and more versatile syslog-ng (next generation); logrotate (for managing log files once written); as well as future directions in Linux logging such as evlog, the enterprise logging facility brought from AIX by IBM.

## Why Log?

Logging is the only way to find out what your system and processes are doing. Linux, like any other Unix system, takes logging very seriously, and regardless of whether you are an administrator or a home user, you will have to deal with system logs at one point or another.

Most logs are written to the /var/log directory. This is the standard practice you will find in Linux text. Log files themselves contain information in a semi-standardized fashion, so it is usually the case if you know how to read one type of log file, you can read them all. Disseminating the information that is logged is something that is specific to the facility that logged the message. In this chapter, we talk briefly about the most popular system logging processes such as kernel, mail, and authentication errors, because most people need to understand what they are to be able to act upon those messages.

# CHAPTER 7

### In This Chapter

- Explaining log files
- Using various loggers
- Managing log files

## The Files in /var/log

Our initialization was based on the default, so the contents of /var/log should be very similar to what we will talk about in this section. If you have installed other applications, such as Samba or BIND, you will find more logs on your system.

Core services such as Apache, Samba, and BIND log to a subdirectory under /var/log can grow quite large, and the subdirectory structure provides a more structured view of your system. Having a single directory for all your applications log can prove confusing, especially when applications write more than one log per file. Listing 7-1 shows a long list of /var/log file on our default system using the -l command.

## Listing 7-1 : Listing of /var/log

```
ls /var/log -l
total 828
dr-xr-- 2 root root     48 2004-04-05 13:33 apache2
-rw-r-- 1 root root      0 2004-07-30 07:42 boot.log
-rw-r-- 1 root root  17886 2004-08-03 06:05 boot.msg
-rw-r-- 1 root root  20540 2004-08-20 06:06 omsg.msg
-rw-rw- 1 root root    586 2004-07-30 07:42 convert_for.log
dr-xr-x 2 lp root        0 2004-07-30 13:08 cups
-rw-r-- 1 root root  24024 2004-08-26 06:05 faillog
dr-xr-x 2 root root     48 2004-04-05 18:27 kern
-rw-r-- 1 root root   89292 2004-08-03 22:16 kdm.log
-rw-rw- 1 root root  11228 2004-08-10 21:54 localmessages
-rw-r-- 1 root root  12563 2004-08-30 06:05 mail
-rw-r-- 1 root root    276 2004-07-30 19:06 mail.err
-rw-r-- 1 root root  12563 2004-08-30 06:05 mail.info
-rw-r-- 1 root root   2143 2004-07-30 19:06 mail.wall
-rw-r-- 1 root root 164497 2004-08-30 06:05 messages
dr-xr-x 4 news     272 2004-07-30 07:41 news
dr-xr-x 1 root root        0 2004-07-30 09:03 not
dr-xr-x 2 root root        0 2004-07-21 01:01 amba
dr-xr-x 1 root root   70421 2004-08-31 22:15 Sax.log
-rw-r-- 1 root root   1876 2004-08-08 17:45 scmps
dr-xr-x 2 squid root     48 2004-04-06 10:54 system
-rw-r-- 1 root root  15426 2004-07-30 18:57 update-messages
dr-xr-x 2 root root     48 2004-04-05 10:18 vbox
dr-rw-rw 1 root root   12756 2004-08-30 06:05 wmtmp
dr-rw-rw 1 root users   26764 2004-08-30 06:05 wtmp
-rw-r-- 1 root root  24358 2004-08-20 06:05 Free866.log
dr-xr-x 1 root root     15 2004-04-10 05:30 xvt
dr-xr-x 2 root root     352 2004-07-30 18:55 YaSt2.
```

The names of most of the entries in this directory indicate the contents of each log file or the program or type of program that created them. For example, mail refers to the Mail Transfer Agent (MTA) such as Postfix or sendmail that is running on your system. In much the same way, if you had Apache on your system, you would find an /var/log subdirectory that contains Apache-specific log files.

Most log files do not contain system or private user data so can be read by anybody on the system. Certain files do contain information that should be read only by the superuser on the system and refer to kernel messages, authentication messages, and mail messages. To find out what normal users are able to access the system, do a long listing on the /var/log directory (as we have done in Listing 7-1).

For more information on listing files, see Chapter 13.

## Logging with syslog

The Standard logging facility is syslog. The syslog daemon intercepts messages logged to the system logging facility and then processes those messages based on the configuration specified in /etc/syslog.conf. The other side of syslog is the klog process, the kernel logging process processes kernel-specific messages such as kernel crashes or a failure in a component of the kernel (for example, a kernel module).

Not all processes use the syslog method of logging. You will see in this chapter that syslog has some limitations. To get around them, many applications provide their own logging facilities and use their own logging mechanisms. The way that such applications handle logging is therefore application-specific, and do not use the syslog process.

The configuration file for syslog is relatively simple to read, and you will see why it is limited in use by modern systems based on this.

When a process asks the kernel to log information, it passes a logging facility to the kernel system call. This logging facility tells the kernel and the user what type of log it is. In case of mail, the logging is MAIL. For FTP logging, it would be FTP. A total of 20 logging facilities are available to the system, 12 of which are used for specific purposes (see Table 7-1) and 8 for local use. (When we talk about local use, we mean that you can tell your application to use one of the local logging facilities to customize how those log entries are saved and interpreted).
