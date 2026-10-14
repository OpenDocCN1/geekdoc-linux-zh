early-warning indicators of an impending attack: Often you will see “probes” over a period of days or even weeks before an actual penetration attempt takes place.

# NOTE

You can find discussions about log file maintenance, log parsing automation, and alerts in Chapter 12.

After an incident has occurred, good logs can help you determine how the attack was launched and what systems may have been compromised. In addition, the logs may even indicate the source (or the “alleged” source) of the intrusion. Because hackers know the values of these log files, they often wipe out or alter the logs, as well as install a Trojan logging daemon, to cover their tracks. To counter this compromise to your system, centralized logging could save the day. After all, if a machine is compromised but the log evidence isn’t kept on that machine, it is going to be much more difficult for the intruder to cover his tracks. In addition to the extra level of protection, monitoring the logs for the whole network is also much easier when they are all located in one place.

# TIP

By default, syslog messages are stored in various files in /var/log. However, you can change the filenames and locations by modifying /etc/syslog.conf.

syslog is the tried-and-true workhorse of Unix logging utilities, and it is not surprising that it is also used on Linux. syslog accepts log data from the kernel (by way of klogd), from any and all local processes, and even from processes on remote systems. As part of the SLES base system installation, syslogd is preconfigured to use the local host as the receiver.

To set up a central syslog server, simply start syslogd with the -r switch, which tells it to listen for messages from remote machines on UDP port 514. On an SLES 9 server, syslogd is set up to automatically start at system boot, and the script used is /etc/init.d/syslog. The startup references /etc/sysconfig/syslog for a few variable settings, including SYSLOGD_PARAMS. Therefore, you should modify /etc/sysconfig/syslog and add -r to the SYS-LOGD_PARAMS line, as follows:

```
SYSLOGD_PARAMS="-r"
```

Then restart syslogd using the /etc/init.d/syslog restart or /sbin/rcsyslog restart command.