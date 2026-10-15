of other services under inetd deteriorates. This is so because, with a higher number of slave processes serving the clients for a particular service, inetd has to multiplex a greater number of sockets associated with the slave processes. This means longer average waiting times for other services. Under these scenarios, you should remove such services from inetd.

We discuss briefly how inetd works, the kind of services it offers, and how you can change the set of services that it offers. On some UNIX systems, the tcpwrapper package is used to enhance the security of inetd, and on other UNIX systems this functionality is built into inetd.

# 20.10.1 Managing inetd on Solaris via Service Management Facility

The inetd daemon is invoked at system start-up time, and is configured via Oracle Solaris service management facility (SMF). We give a brief description and usage example of SMF with respect to inetd, particularly the svcadm command and its options in Sections 23.2.5.4, 23.2.5.4.2, and 23.2.5.5.

The SMF framework manages system and application services. SMF manages critical system services essential to the working operation of the system and manages application services such as databases or Web servers. SMF improves the availability of a system by ensuring that essential system and application services run continuously, even in the event of hardware or software failures.

SMF replaces the use of configuration files for managing services and is the recommended mechanism to use to start applications. SMF replaces the init scripting start-up mechanism, inetd.conf configurations, and most rc.d scripts. SMF preserves compatibility with existing administrative practices wherever possible.

The SMF command line utility that controls and configures inetd services is named inetadm. The inetadm command is used to monitor, configure, and control inetd services. If you type inetadm on the command line, you get a complete listing of inetd services, their properties, and values.

The contents of the file /etc/services lists the ports that the network services use. It would be very instructive for you to scroll through the content of the /etc/services file to learn what services are provided on what ports on your Solaris system.

See the inetd and inetadm manual page in Solaris for more details on how to manage inetd services. If necessary, you can use the inetconv command to convert an inetd configuration file content into SMF format services, and then manage these services using inetadm and svcadm commands.

# 20.10.1.1 Configuring inetd on PC-BSD

The /etc/inetd.conf file contains the list of services offered by inetd on a UNIX system. It is a text file that contains one seven-field line per service, having the following format:

```
service-name socket-type protocol wait/nowait user:group server-program arguments
```

Each of the services listed in /etc/inetd.conf must also be recorded in the /etc/services file. Table 20.24 contains the purpose of each field.