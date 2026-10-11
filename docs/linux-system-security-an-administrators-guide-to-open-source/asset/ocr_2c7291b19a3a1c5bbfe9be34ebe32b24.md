syslogd. This mechanism provides a way of capturing items of particular interest and acting on them in ways not supported directly by *syslog*, such as generating e-mail or generating a page through a modem. We will look at managing the log messages and log files in detail in Chapter 17.

# Invoking the **syslogd** Daemon

The **syslogd** daemon is invoked by the script **/etc/rc.d/init.d/syslog** at run level 2. By default, it is invoked with no options. There are two options that are of interest and may be necessary for the proper configuration of your environment—the **-r** and **-h** flags.

If you are going to use a log server, then you must invoke **syslogd** -r. By default, **syslogd** will not accept log messages from remote systems. By specifying the **-r** option, **syslogd** will listen to incoming UDP packets on port 514. Whenever a log message is received from another host, */etc/syslog.conf* will direct **syslogd** as to how to handle the message. The hostname of the remote system will be prefixed to the log message before it is written. If */etc/syslog.conf* does not contain a selector and action for the incoming message, then the message is dropped. The topic of a centralized log server is further discussed in *Logging to a Central Server* on page 167.

If you additionally want the log server to forward log messages, then you must use the **-h** flag. By default, **syslogd** will ignore */etc/syslog.conf* entries that would cause it to forward a log message from a remote system to another remote system.

# Configuring **/etc/syslog.conf**

The most important aspect of configuring the */etc/syslog.conf* file is thinking through what you want to get out of it. In other words, what messages do you want, how do you want them processed, and how quickly do you want them? As you read through the remainder of this book, exactly what you want will become clearer. As you work with **syslog** and the information it generates, you will evolve to a zen state, wherein you begin to visualize the output of **syslog** before you have implemented it!

Let’s begin by taking a look at a representative **/etc/syslog.conf** file in Example 8-1. This happens to be the **/etc/syslog.conf** file as it ships with Red Hat 5.2 (well, almost, anyway—the line containing @central is not there by default). Notice that the record beginning with **kern.** is commented out. If you uncomment this line, then all kernel messages at all levels will be written to the system console.

Most of the log messages, based on the entries in Example 8-1, will end up in **/var/log/messages**. This is due to the line beginning with *info; mail; authpriv;none*, which means that messages from all facilities at level *info* and higher except *mail* and *authpriv* messages will be written to