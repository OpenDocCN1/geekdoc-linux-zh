
aliases file contains a list of alternate names or e-mail addresses to which e-mail messages might be addressed. Each e-mail alias in this file is followed by text that defines what sendmail should do with a message so addressed. For example, suppose that your e-mail address is kcarver@myplace.net. Because different companies use specific formats for e-mail addresses, you would also like to receive e-mail using the following e-mail addresses: kim.carver@myplace.net, kim_carver@myplace.net, and kimc@myplace.net. Using e-mail aliases lets you do this if you include the following lines in /etc/aliases:

```
kim.carver: kcarver
kim_carver: kcarver
kimc: kcarver
```

Aliases are also commonly used for assigning topical e-mail to a specific individual. For example, you can define a webmaster alias that sends e-mail to the accounts of Kim Carver and Thomas Jennings, who work at a company that helps manage your Web server:

```
webmaster: kcarver, tjennings@webstuff.com
```

Each time you make a change in /etc/aliases, you must run the newaliases command to create a database of aliases that sendmail can use. This is done automatically each time sendmail is started, but you can rebuild the database with newaliases at any time without restarting sendmail.

Individual users can't alter the /etc/aliases file, but they can create a .forward file in their home directories. If sendmail finds a .forward file in a user's home directory, e-mail for that user is processed according to the text in .forward instead of simply being sent to the user's standard inbox in /var/spool/mail. Common uses of .forward include forwarding e-mail to another system when you prefer to receive your e-mail at another host (this method requires you to have a user account on the e-mail server) and piping your messages through a mail filter to remove spam or sort messages. For example, if you were on assignment with a subsidiary company for a month, you could include the following line in your .forward file:

```
kcarver@myplace_germany.net
```

All e-mail that would have been delivered to your mailbox is instead forwarded to the e-mail address given.

## Watching sendmail Work

The sendmail daemon creates copious logs of what it does. Each message received and each message sent out are logged along with daemon-specific messages about the server configuration, starting and stopping, and so on. These messages are written to the standard system logger, syslogd, based on the configuration in /etc/syslog.conf. The default setting in Red Hat Linux and Fedora is to store messages from any mail server in /var/log/maillog.

In addition to learning about sendmail activity by reviewing the log files, you can use several other programs that will keep you informed about the state of your e-mail server, such as:

- hoststat: Displays the status of hosts that have recently sent e-mail to your sendmail daemon. By default, information for a host is maintained for 30 minutes.
- mailq: Displays a list of messages waiting to be sent out. Messages wait in the queue while you are not connected to the Internet, while sendmail waits for a domain name to be resolved, or a message has not been accepted by a remote mail server (by default, sendmail will try again later).
- mailstats: Displays a summary of the amount of e-mail traffic that sendmail has handled. Fields in the output of mailstats include messages received, bytes received, messages sent, bytes sent, messages rejected, and messages discarded.

## Using Superservers for Network Services

On a Linux system providing many network services, it can be wasteful to have 30 or more different services running at the same time. Many services are only needed occasionally. Yet you still want client requests for each service to be handled without you intervening to start the needed service. The solution is the superserver (also called a metaserver), which listens on multiple network ports and starts the appropriate service when a client connection arrives for that port. The most widely used superserver program is called inetd, for Internet daemon. Another superserver that is gaining in popularity is xinetd, for extended Internet daemon. xinetd is used by default on Red Hat Linux and Fedora.

![](img/43f64015de86d989e30eff5bb284fb96_748_0.png)

> Some network services do not rely on the superserver mechanism; they are designed to run in standalone mode, without being started by inetd or xinetd as new client requests arrive.

Examples of network services that often rely on a superserver are FTP, Telnet, SSH, and standard e-mail servers. The mapping of services to default port numbers is done via the /etc/services file.

Many different programs refer to /etc/services to determine which port to use for a particular network service. The superserver daemons use the port numbers in /etc/services to determine which ports to watch for client connections. When a client tries to connect to a given port number, the superserver starts the appropriate network service to handle the client's request. After that request has been handled, the network service exits, so its resources are freed for other programs. The only program that has to be running all the time is the superserver itself.

Both inetd and xinetd are configured using text files within /etc. The configuration files indicates to which ports the superserver should listen and which program the superserver should start if a client request arrives on one of those ports. xinetd has a more complex configuration model and better security, though inetd is perfectly adequate when used in conjunction with certain security measures you'll learn about in the next section.

## Using xinetd

The xinetd program is a revised version of inetd that focuses on creating a more secure environment, and happens to be more sound in its configuration architecture as well. xinetd as shipped with Red Hat Linux and Fedora (which do not include inetd) includes a configuration file /etc/xinetd.conf that refers to the contents of the /etc/xinetd.d directory. Within that directory, each service is configured by a separate file. A sample file, /etc/xinetd.d/wu-ftpd, is shown here:

```
# default: on
# description: The wu-ftpd FTP server serves FTP connections.
It uses \
#normal, unencrypted usernames and passwords for authentication.
service ftp
{
socket_type= stream
wait= no
user= root
server= /usr/sbin/in.ftpd
server_args= -l -a
log_on_success+= DURATION USERID
log_on_failure+= USERID
nice= 10
disable= yes
}
```

The format of each file in /etc/xinetd.d names a service, as in the service line above. Brackets then enclose options that apply to that service. Some of these options match those described in the next section for the inetd.conf file, such as socket_type, user, and server. Several other options extend the functionality of xinetd beyond what the older inetd program offers. For example, various logging options are provided to determine what information xinetd writes to the system log when a connection is attempted, and several security options are available to control access to services. For example, the parameters only_from, no_access, access_time, and deny_time determine which hosts can access a service and when they can access it.

The extensive man page for xinetd.conf describes its available options. One particular option to note is the disable option. Several services in Red Hat Linux are fully configured but are disabled, so no connections are accepted. You can enable them by changing the line in the appropriate configuration file to disable=no. By default, the configuration files located in /etc/xinetd.d/ in Red Hat Linux include the line disable=yes so that the service is not active (available to clients) until you manually alter this default setting.

You should also restart xinetd after making any changes to its configuration files:

```
# service xinetd restart
```

## Using inetd

The inetd program is configured using /etc/inetd.conf. A few sample lines from this file are shown here:

```
ftp      stream  tcp     nowait  root    /usr/sbin/tcpd in.ftpd -l -a
telnet   stream  tcp     nowait  root    /usr/sbin/tcpd in.telnetd
```
