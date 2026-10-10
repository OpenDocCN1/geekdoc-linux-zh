# Setup

This task requires no special setup. You need `root` access to your computer, though. To redirect logging to another system, you need working network access and the other computer must be configured to accept system logs from remote computers.

# Caveats

As usual, *working as `root`* is potentially risky. For security reasons, most log files can only be read by `root`, so you need `root` access even if you don’t intend to change your configuration. Misconfiguring your log files can result in system logs disappearing or being sent to inappropriate files or remote systems.

# Procedure

Before actually configuring your system logging options, you should know a bit about the programs that manage it—particularly `syslogd` and related tools. With the basics under your belt, you can adjust the syslog configuration files as well as the files that manage log file rotation. You can examine log files using tools with which you’re already familiar, such as `grep` and `less`, although a few twists are particularly handy when studying log files.

# Understanding `syslogd`

The traditional Linux system logger is `syslogd`, which is often installed from a package called `sysklogd`. The `syslogd` daemon handles messages from servers and other user-mode programs. It’s usually paired with a daemon called `klogd`, which is usually installed from the same `sysklogd` package as `syslogd`. The `klogd` daemon manages logging of kernel messages.

> NOTE
> Other choices for system loggers exist. For instance, syslog-ng is a replacement that supports advanced filtering options, and meta1og is another option.
> 
> This chapter describes the traditional `syslogd` logger. Others are similar in principle, and even in some specific features, but differ in many details.

The basic idea behind a system logger is to provide a unified means of handling log files. The daemon runs in the background and accepts data delivered from servers and other programs that are configured to use it. The daemon can then use information provided by the server to classify the message and direct it to an appropriate log file. This configuration enables you to consolidate messages from various servers in a handful of standard log files, which can be much easier to use and manage than potentially dozens of log files from the various servers running on the system.

In order to work, of course, the log daemon must be configured. In the case of `syslogd`, this is done through the `/etc/syslog.conf` file. The next section describes this file’s format in more detail.