
## PART III

## Data Backup and Disaster Recovery

- 8. Network Services
- 9. Printing Services
- 10. Data Backup and Recovery

## Network Services

One major strength of Linux is in its offering of a wide range of network services. SLES 9 ships with a large number of such services, ranging from network time services to file sharing to web page serving. A detailed discussion of each topic discussed in this chapter is not feasible due to space; entire books are devoted to many of the topics, such as the Domain Name Service (DNS) and Samba. Therefore, the intention of this chapter is to provide you with the bare necessities to get a specific network service configured and running with a basic configuration.

We selected the topics covered here because they provide services to users on your local, private network, and not necessarily services over the Internet. This is why certain topics, such as the Squid proxy server and SuSEfirewall2, are not discussed here. The following topics, however, are discussed in this chapter:

- The xinetd super-server
- The Network Time Protocol (NTP) service
- Email services using Postfix
- FTP services
- File sharing using NFS and Samba
- Remote management using VNC, XDMCP, and Telnet/ssh
- Network name services using DNS, DHCP, SLP, and Samba
- Web page serving using Apache
- Authentication services using Kerberos, LDAP, NIS, and Samba

There are other services beyond those available with SLES. Novell's Open Enterprise Server (www.novell.com/products/openenterprise) provides a number of extra services (such as NetStorage and iFolder) that help bring the Novell and SLES world closer. These extra services are, however, beyond the scope of this chapter.

## Angels and Daemons

Because SLES multitasks, there are always some programs running in the background that take care of the system-related tasks, such as executing cron and at jobs and watching out for and servicing network requests. These background processes are referred to as daemons.

### THE ORIGIN OF THE WORD DAEMON

Some references indicate daemon (pronounced dee-man or day-man) is an acronym for Disk And Execution Monitor. However, the word was actually first used by Professor Fernando J. Corbato and his Project MAC (http://en.wikipedia.org/wiki/MIT_Laboratory_for_Computer_Science) team back in 1963 to reference the background processes on the IBM 7094 mainframe. The reference was inspired by one of the “thought experiments” about thermodynamics conducted by the famous nineteenth century Scottish physicist James Clerk Maxwell (famous for Maxwell’s equations of electrodynamics). In this experiment, Maxwell suggested that there exists an imaginary agent (a daemon) that helped sort molecules of different speeds and worked tirelessly in the background—an apt analogy to the various housekeeping tasks inside a multitasking computer operating system. (Visit http://ei.cs.vt.edu/~history/Daemon.html for more information.)

The Unix community adopted use of the word daemon, which in Greek mythology is a supernatural being that exists between gods and men, to describe the various background server processes that serve users (men) on behalf of the kernel (god). As a result, most of the server applications (such as the FTP server) have d appended to their filename—for example, ftpd; this serves to separate them from the client applications (such as ftp for the FTP client).

Instead of having various server services (such as FTP) started at system initialization time (which would slow down the server boot process) and be dormant until a connection request arrives (taking up unnecessary resources), a special daemon process is started and listens on all service ports for the services listed in its configuration file. When a request comes in on a port for which there is an “active” server listed in the configuration file, this monitor daemon starts the appropriate server. Furthermore, this monitor daemon can provide additional security if the service does not. Because of the way this server operates, it is generally referred to as the super-server. The drawback of running a frequently accessed service under the super-server is the slight delay caused by the super-server in starting up the service every time it is required.

There are two implementations of this super-server: inetd (Internet services daemon; pronounced eye-net-d) and xinetd (Extended Internet services daemon; pronounced zye-net-d). inetd has been widely used since the early days of Unix. However, in recent years, xinetd is much more popular due to its extended functions such as access logging, enhanced access control, and IPv6 support. For example, although inetd allows control for TCP connections using Wietse Venema’s TCP_Wrappers software (tcpd, which is included on your SuSE Linux media), you cannot control UDP connections. Although you can control the rate of connections using inetd, you cannot control the maximum number of instances. This could lead to process table overflow attacks—for example, an effective denial of service (DoS). xinetd does not suffer from these shortcomings. By default, SuSE 9 uses xinetd instead of inetd, so that is what we discuss here.

**TIP**

If you have been using inetd and want to convert over to xinetd, use either the itox utility or the xconv.pl Perl script (both supplied with xinetd, but xconv.pl is generally preferred over itox) to convert your inetd.conf style configuration files to xinetd.conf. Refer to man itox and man xconv.pl for more information.

### Configuring xinetd

On startup, xinetd reads several files located in /etc. The main configuration files are /etc/xinetd.conf plus all files in /etc/xinetd.d. The other files specify which daemon should be started for which service. The other files it reads are shared with other daemons and system services and contain more general information about Internet services:

- **/etc/services**—This file maps port numbers to service names. Most of the port numbers below 1024 are assigned to special (so-called well-known) services (see http://www.iana.org/assignments/port-numbers) and are listed in this file. Every time you refer to a service by its name (as opposed to its port number), the name is looked up in /etc/services and the assigned port number is used to process the request.
- **/etc/protocols**—This file maps protocols to the numbers the kernel uses to distinguish between the different TCP/IP protocols. The list is based on http://www.iana.org/assignments/protocol-numbers.
- **/etc/rpc**—Similar to /etc/services, this file maps Remote Procedure Call (RPC) services to their ID numbers and common names.

Generally, you don't need to touch any of the files in the preceding list. When you do, the likely candidate for changes is `/etc/services`, where you'll add the port(s) used by some custom daemons not already listed in the file or if you need a specific service to run on a port other than its accepted default for some reason.

You can configure services supported by `xinetd` in two ways: using YaST or working directly with the configuration files. Although YaST provides a friendly user interface, you can modify certain options only by editing the configuration files directly. Therefore, we cover both procedures here.

To access the `xinetd` configuration module in YaST (see Figure 8.1), select Control Center, Network Services, Network Services (inetd). Alternatively, you can access this module directly by using `yast2 inetd` or `yast inetd`. Note that some of the menu text shows `inetd` even though you are using `xinetd`.

**FIGURE 8.1**

The xinetd configuration screen.

![](img/ae8469257d2662b469f2360b3bbbe322_241_0.png)

The top of the screen shows whether the super-server is running (Enabled) or not (Disabled). The list box on the screen shows the defined services and their current run status. Of particular interest are the columns labeled Ch, Status, and Server.
