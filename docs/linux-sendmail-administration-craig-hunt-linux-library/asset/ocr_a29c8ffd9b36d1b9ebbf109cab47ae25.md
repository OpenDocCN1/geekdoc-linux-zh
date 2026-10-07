# Basic Security

The other way to limit the software on a system is to remove it after it is installed. For example, to remove FTP from a system with rpm you could enter:

```
rpm -e ftp-0.017-6
```

Package managers like RPM and dpkg are very effective and easy to use. Removing software without a package manager can be difficult, particularly if unanticipated software dependencies arise. From a security perspective, the role that package managers play in removing software is just as important as the role they play in installing software.

# Disabling Unneeded Software

It is not necessary to remove software in order to prevent it from running. Sometimes you want to keep software so that it can be enabled for special occasions. Other times you want to evaluate the impact before removing software. If you're not sure you want to remove a network daemon, by disabling it until you are sure that doing so has no negative impact on your users or your server. There are two simple ways to prevent daemons from running.

Remove unneeded daemons from the inetd or xinetd configuration Most network services are started by inetd. The services are started in inetd.conf. Removing a service from the file prevents outsiders from using the specified network service does not block you from using the service on outbound connections. Thus, if ftp is deleted from inetd.conf, you can still ftp to remote sites but no one from a remote site can use ftp to connect into your server.

xinetd is an alternative to inetd that is used on some Linux distributions, notably Red Hat 7. xinetd starts the services listed in the /etc/xinetd.conf file. in the Red Hat 7 configuration, xinetd.conf includes reference all of the scripts defined in the directory /etc/xinetd.d. To disable an unneeded daemon in Red Hat 7, use the same chkconfig command to control boot scripts. For example, to disable rlogin, enter chkconfig rlogin off at the command prompt.

Remove start-up scripts that launch unneeded services Networkmail is a good example—are started at boot time. Use chconfig, tksystem, and a similar tool to remove unneeded daemons from the start-up. For example, your Sendmail server may not need to run the httpd start-up script because it is not a Web server. You're still able to use a Web browser even if the httpd script is not run at start-up.

In addition to installing the latest software updates and removing unneeded software, limit access to the software and services running on your server to just those systems that

![](bbox=[0.91, 0.583, 0.985, 0.653])

PART 4