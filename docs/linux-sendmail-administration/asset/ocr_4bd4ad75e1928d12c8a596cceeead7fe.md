# Basic Security 327

The other way to limit the software on a system is to remove it after it is installed. For example, to remove FTP from a system with rpm you could enter:

```
rpm -e ftp-0.01-6
```

Package managers such as RPM and dpkg are very effective and easy to use. Removing software without a package manager can be difficult, particularly if unanticipated software dependencies arise. From a system security perspective, the role that package managers play in removing software is just important as the role they play in installing software.

# Disabling Unneeded Software

It is necessary to remove software in order to prevent it from running. Sometimes you want to keep software so that it can be enabled for special occasions. Other times you want to evaluate the impact before removing software. If you're not sure you want to remove a network daemon, by disabling it until you are doing so has no negative impact on your users or your server. There are two simple ways to prevent daemons from running:

Remove unneeded daemons from the inetet or xinetd configuration Most network services are started by inetet. The services it starts are listed in inetet.conf. Removing a service from the file prevents outsiders from using the specified network service does not block you from using the service on outbound connections. Thus, if ftp is deleted from inetet.conf, you can still use ftp to remote sites but no one from a remote site can use ftp to connect to your server.

xinetd is an alternative to inetet that is used on some Linux distributions, notably Red Hat 7. xinetd starts the services listed in /etc/xinetd.conf file. In the Red Hat 7 configuration, xinetd.conf includes reference to all of the scripts defined in the directory /etc/xinetd. To disable an unneeded daemon in Red Hat 7, use the chkconfig command that is used to control boot scripts. For example, to disable rlogin, enter chkconfig login off at the command prompt.

Remove start-up scripts Some network services—Sendmail is a good example—are started at boot time. Use chkconfig, tkconfig, or a similar tool to remove unneeded daemons from the start-up. For example, your may not need to run the httpd start-up script because it is not a Web server. You're still able to use a Web browser if the httpd script is not run at start-up.

In addition to installing the latest software updates and removing unneeded software, limit access to the software and services running on your server to just those systems that

![](bbox=[0.913, 0.577, 0.995, 0.693])