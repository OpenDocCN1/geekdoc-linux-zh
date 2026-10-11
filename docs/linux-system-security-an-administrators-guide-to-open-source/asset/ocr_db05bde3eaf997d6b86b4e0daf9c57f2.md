# Wiretapping Is Not So Much Fun, After All!

# Log File Management

Throughout this book, we've been discussing log files and telling you how important it is to read them. Log files record information that can typically be boring but sometimes is extremely important. For example, you may be experiencing a hardware failure, misconfiguration, or an intrusion. Frequent review of your log files helps you learn information like this the easy way rather than the hard way.

You also need to make sure you reset your logs and cycle out the old ones periodically so that your disk doesn't fill up. Proper management of your log files ensures that they are available when you need them. If you back up your log files regularly with the rest of your system, you extend the availability of this audit information.

All these things may seem like tedious work, but there are a few tools that can help. We'll cover `logrotate`, `swatch`, and `logcheck` in this chapter. Each of these tools does one thing particularly well, and using them all helps to add layers of protection to your system.

# GENERAL LOG FILE MANAGEMENT

You should log as much information as you can to your log files. Chapter 8 discusses the configuration of the `syslog` utility. In particular, *Logging to a Central Server* on page 167 describes the configuration and security requirements for centralized logging. Logging to a central, secure server can greatly ease log