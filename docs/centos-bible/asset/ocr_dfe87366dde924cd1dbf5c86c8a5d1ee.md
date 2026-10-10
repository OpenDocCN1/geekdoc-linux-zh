service may be easier than typing in a long list of subnets or domains, but better a few minutes spent on proper security measures than many hours recovering from a break-in.

> You can further restrict access to services using various options within the `/etc/xinetd.conf` file, even to the point of limiting access to certain services to specific times of the day. Read the manual page for xinetd by typing `man xinetd` at a command prompt) to learn more about these options.

# ## Checking Log Files

Preparing your system for a cracker attack is only part of the battle. You must also recognize a cracker attack when it is occurring. Understanding the various log files in which CentOS records important events is critical to this goal. The log files for your CentOS system can be found in the `/var/log` directory.

Because the system logs are plaintext files, you can view the contents of logs directly using any text editor or paging command (such as `less` or `more`). The `logwatch` facility that comes with CentOS sends daily highlights from your log files in an e-mail message to the `root` user. You can also add packages, such as `logsentry`, to monitor your log files.

# ## Replacing the `syslogd` Package

The default logging service in CentOS is `syslogd`. However, the newer `rsyslogd` is more flexible and powerful than its predecessor. I suggest that you install and use `rsyslogd`, and uninstall `syslogd`. You can do this at a Terminal window as `root` user.

```
`# yum install rsyslog && yum remove syslogd`
```

The `&&` is very important because removing the `syslogd` package without having a `syslog` replacement will remove most of your system!

After the `rsyslog` package has been installed with `yum`, you need to enable it with `chkconfig` and start the service.

```
`# service rsyslog start`
`# chkconfig rsyslog on`
```

# ## Understanding the `rsyslogd` Service

Most of the files in the `/var/log` directory are maintained by the `rsyslogd` service. The `rsyslogd` daemon is the System Logging Daemon and acts as an extension of a previous logging system called `syslogd`. It accepts log messages from a variety of other programs and writes them to the appropriate log files. This is better than having every program write directly to its own log file because it allows you to centrally manage how log files are handled. It is possible to