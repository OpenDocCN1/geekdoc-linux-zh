
## Output Examples

You may also want to write your own scripts or programs or use other (besides logcheck and swatch) existing ones to capture certain types of activity. Example 8-3 shows a sequence of failed login attempts as reported by login and PAM to syslogd (line wraps are due to formatting constraints), which may represent an attempted break-in.

### Example 8-3 Failed login Attempts Using the Same Username

```
Mar  2 17:54:15 topcat login[14435]: FAILED LOGIN 1 FROM roadrunner FOR guest, Authentication failure
Mar  2 17:54:23 topcat login[14435]: FAILED LOGIN 2 FROM roadrunner FOR guest, Authentication failure
Mar  2 17:54:28 topcat login[14435]: TOO MANY LOGIN TRIES (3) FROM roadrunner FOR guest, Have exhausted maximum number of retries for service.
Mar  2 17:54:28 topcat PAM_pwdb[14435]: 3 authentication failures; (uid=0) -> guest for login service
```

Be aware, however, that different attacks will generate different log entries (often called signatures). Unfortunately, collecting a thorough list (it will never be complete!) of attack patterns is difficult due to the dynamic nature of attacks. The process of identifying attacks is known as intrusion detection. The section Intrusion Detection on page 172 provides some resources related to that topic. In the meantime, Example 8-4 shows us a different set of failed login attempts (line wraps).

### Example 8-4 Failed login Attempts Using Different Usernames

```
Mar  2 18:00:10 topcat login[14478]: FAILED LOGIN 1 FROM roadrunner FOR guest, Authentication failure
Mar  2 18:00:16 topcat login[14478]: FAILED LOGIN 2 FROM roadrunner FOR joe, Authentication failure
Mar  2 18:00:20 topcat login[14478]: FAILED LOGIN 3 FROM roadrunner FOR mary, Authentication failure
Mar  2 18:00:24 topcat login[14478]: FAILED LOGIN SESSION FROM roadrunner FOR sdm, Authentication failure
Mar  2 18:00:24 topcat PAM_pwdb[14478]: 1 authentication failure; (uid=0) -> sdm for login service
Mar  2 18:00:24 topcat PAM_pwdb[14478]: 1 authentication failure; (uid=0) -> mary for login service
Mar  2 18:00:24 topcat PAM_pwdb[14478]: 1 authentication failure; (uid=0) -> joe for login service
Mar  2 18:00:24 topcat PAM_pwdb[14478]: 1 authentication failure; (uid=0) -> guest for login service
```

The important thing about Examples 8-3 and 8-4 is to notice any similar key words or phrases that could be used in writing a script to capture these break-in attempts. In this case, notice that, although these two examples show different log entries for the two attacks, the process identifier (the number in brackets after either the keyword login or PAM_pwdb) is identical for each sequence of attacks. That, together with the fact that the key phrase authentication failure appears in almost every entry associated with these attacks, makes writing a script to capture this information fairly straightforward (of course, in Example 8-3 it could simply be a user who forgot his or her password, representing a false alarm). If you do decide to write your own scripts and/or programs, take advantage of the ones that already exist. Read through them and benefit from the experience—and mistakes—of others.

## The klogd Daemon

The klogd daemon captures and logs Linux kernel messages. Normally, it submits all messages to syslog for logging. However, if invoked with the -t *filename* argument, it will log all of its messages to *filename* instead of passing them to *syslog*. When an alternate file is specified for logging, klogd reports all levels or priorities to the file. There is no configuration file for klogd equivalent to /etc/syslogd.conf. The advantage of having klogd avoid syslogd is largely for debugging. However, if someone has hacked your kernel, it may be that using this facility will assist in determining the modifications. If you are familiar with the kernel and its source code, this may be valuable. If not, once you've determined that your kernel has been modified in an unauthorized way, it is probably best to recover from pristine backups (discussed in Chapter 3).

> **NOTE**
>
> Both syslogd and klogd are started when the system enters run level 2. They are killed when the system goes down to run level 1. The controlling script on Red Hat 5.2/6.0 is /etc/rc.d/init.d/syslog.

## OTHER LOGS

You will find a number of other log files in /var/log and potentially elsewhere on your system depending on the distribution you have and the applications you have configured. Of course /etc/syslog.conf will list the names and locations of all log files managed by syslogd. Others will be managed by other applications. For example, on Red Hat 5.2/6.0, the Apache Web Server generates the /var/log/htaccess.log file to record client access, as well as /var/log/httpd/error.log to capture error conditions outside of syslog. The cron utility maintains its own informational log file, /var/log/cron. The linuxconf utility will generate log files such as /var/log/netconf.log whenever it records system reconfiguration information. Samba (a Server Message Block (SMB) based utility similar to NFS in functionality) maintains its log files in the /var/log/samba directory. You will find another set of files in /var/log related to connection and process accounting. These files include wtmp, paccct, and lastlog, each of which is discussed in Chapter 7.

Many of these files contain security-related information and therefore require your attention. The standard log files are discussed at various points within this text; others will be application and site dependent.

## ALTERNATIVES TO syslog

It is possible on very busy systems for syslogd to lose messages. On such systems you may want to take a look at cyclog. It is a syslogd replacement that buffers log messages and makes sure that the log files are synchronized. It also automatically rotates the log files it manages. It is a part of the daemontools collection of utilities and is available from

```
ftp://koocbera.math.umich.edu/ww/daemon-tools.html
```

## THE AUDIT UTILITY

One publicly available tool that is quite useful for capturing system activity beyond that of syslogd or system accounting (discussed in Chapter 7) is auditd. This utility is available from

```
ftp://ftp.tet.org/pub/linux/auditd/
```

This utility allows for the capturing of various system events, such as e-mail, in-bound and out-bound network connections, logins, su usage, file access, and kernel module changes. Unlike syslogd, which depends on other processes to generate messages, auditd captures system calls in the kernel based on a configuration file. It is similar to the Basic Security Module (BSM) found in IRIX 6.5.x, Solaris 2.x, or the Security Audit Trail (SAT) found in IRIX 6.5.x.

The auditd utility can generate a reasonably complete audit trail of the system it runs on. This level of detail is useful for systems that are exposed to the Internet, such as firewalls, web servers, and ftp servers. It is also advantageous to run this utility on internal systems that contain sensitive data.

Installing this tool will require a rebuild of the kernel, so make sure that you read the on-line documents /usr/src/linux/README and /usr/doc/HOWTO/kernel-HOWTO before proceeding with building a Linux kernel for the first time. Rebuilding and Recompiling the Kernel on page 420 in Chapter 15 describes the process of rebuilding the kernel for the Transparent Cryptographic File System (TCFS), and offers a good example.

## SUMMARY

This chapter provides an overview of the syslog utility. We described the operation of syslogd and the configuration file /etc/syslog.conf.

## FOR FURTHER READING

### General System Logging

- Frisch, Aileen, *Essential System Administration*, 2d ed., Sebastopol, California, O’Reilly & Associates, Inc., 1995.
- Hein, Jochen, *Linux Companion for System Administrators*, Harlow, England, Addison-Wesley, 1999.
- Nemeth, Evi, et al., *UNIX System Administration Handbook*, Englewood Cliffs, New Jersey, Prentice Hall PTR, 1995.

### Intrusion Detection

There is an intrusion detection systems (IDS) mailing list. You may subscribe to it by sending e-mail to majordomo@uow.edu.au with subscribe ids in the body of the message.

The IDS frequently asked questions (FAQ) are available at

```
http://www.ticm.com/kb/faq/idsfaq.html
```

A survey of IDS and log management tools may be found at

```
http://www-rnks.informatik.tu-cottbus.de/~schirrey/ids.html
```

For a good overview of intrusion detection, read the book

- Escamilla, Terry, *Intrusion Detection: Network Security beyond the Firewall*, New York, New York, John Wiley & Sons, Inc., 1998.
