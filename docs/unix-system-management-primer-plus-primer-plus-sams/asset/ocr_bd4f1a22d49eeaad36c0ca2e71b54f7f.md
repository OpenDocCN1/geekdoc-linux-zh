# Chapter 6 • MONITORING SERVICES

This limitation can be a real problem during log analysis; Unix systems can be quite verbose in their logging, and the signal-to-noise ratio is often lower than you would like it to be. In addition, many programs hard-code their syslog facility; administrators cannot change the syslog facility to suit their needs. If an FTP server is logging authentications with a facility of daemon, but you want it logged with a facility of auth, you may be out of luck.

Enter syslog-ng in the late 90s. syslog-ng was designed to overcome the limitations in syslog, and it's quickly gaining popularity in the community syslog-ng provides a much more granular filtering mechanism than the everyday syslog, making it a perfect fit for a central log server. For example, you can send all logs coming from a host whose name contains the word "firewall" to a file called firewall. You can send all logs containing the word "log" to a file called auth. syslog-ng even supports a limited set of regular expressions for matching. Of course, you can still filter logs based on priorities.

The configuration of syslog-ng is quite interesting. In its single configuration file, there are five types of directives: options, sources, filters, destinations, and log paths. These directives tell syslog-ng where to find log messages and how to route them to their final destinations. The following sections discuss these directives in detail.

# Options

Options are syslog-ng's global configuration options. You can use options to set the default permissions, owner and group of log files, have syslog-ng automatically create directories for log files, and set the behavior of timestamps (use remote timestamp or the time we received). Other options are also available; you can learn about them by visiting the syslog-ng home page at http://www.balabit.hu/en/downloads/syslog-ng.

A typical options directive looks like this:

```
options {
  chain_hostnames(no);
  use_time_recvd(yes);
  create_dirs(yes);
  owner(root);
  group(system);
  dir_perm(0750);
}
```

# Sources

Sources define all of the mechanisms through which syslog-ng can receive a log. If your system sends logging information through the device /dev/log and through UDF network connections on port 514, you would define those mechanisms as sources. A source directive for a central log server running Solaris 8 might look like this:

```
source src { stream("/dev/log" door("/etc/.syslog_door"); internal();
  udp(port(514)); };
```