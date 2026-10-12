For example, to enable the pop3 daemon on a Linux system, you can either use the simple RPM binary that comes with most installations or download the source from its site at ftp://ftp.eac.washington.edu/pine/. Untar and unzip the source, run the commands necessary to compile the source, and then verify and install the executable in /usr/sbin. In the third field under the port number 110, place the word pop3 or the respective process name. You may wish to add a comment afterward if one is not already there. You can add new daemon processes to ports that are over 1024, but to those ports less than 1024 it is advised to not make any changes. You must conform to standards that have been set for port numbers and the processes affixed to them. If you are installing a new process, such as the Big Brother monitoring system that runs under port 1984, verify the correct settings and then make the correct entry.

# Selecting Entries for the inetd.conf File

The fourth option, /etc/inetd.conf, is closely tied to the previous entries in the /etc/services file. To enable the various daemons when they start up, uncomment the line on which the daemon is located by removing the pound sign preceding the text. Because most Linux distributions have tcp_wrappers installed to add security and to provide added logging to the various processes as they run, you will notice that the /usr/sbin/tcpd daemon is often executed in place of the process itself. The tcpd daemon is a silent port monitor that checks the user's authenticity before executing the process without proper authority.

> NOTE
> Red Hat Linux installs top_wrappers by default during a normal install. Seldom do you find any machine not running top_wrappers. Be sure to enable this utility if you choose a customized or limited setup routine.

The syntax for a sample line in the /etc/inetd.conf file is as follows:

```
service socket-type protocol wait/nowait user server-program server-arguments
```

The service option is taken from the /etc/services file. Anything listed in this file can also be started here. Whether you add a new service manually or if its respective RPM adds the service automatically, the new service must conform to