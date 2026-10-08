
# CHAPTER 13: FINDING AND REPAIRING THE DAMAGE

At this point, you have detected a break-in. If your budget and preparation allowed it, it is assumed that you have switched to “Auxiliary Control,” a Security Backup System (Sec-Back) that is to be used if the primary system is compromised. This will allow you more time to find the damage.

It is assumed that the crackers were possibly able to make themselves root and were clever. This means that you cannot trust anything on the disk or in memory. Hopefully, you ensured that log files were duplicated onto another system that was not penetrated, that you made periodic backups which are kept in secure storage, etc. Techniques for duplicating log files in real time are explained in “The syslogd and klogd Daemons” on page 480.

The topics covered in this chapter include:

- “Check Your /var/log Logs” on page 480
- “The syslogd and klogd Daemons” on page 480
- “Remote Logging” on page 480
- “Interpreting Log File Entries” on page 481
- “Check Other Logs” on page 488
- “Check TCP Wrapper Responses” on page 488
- “How the File System Can Be Damaged” on page 488
- “Planting False Data” on page 489
- “Altered Monitoring Programs” on page 489
- “Stuck in the House of Mirrors” on page 490
- “Getting Back in Control” on page 490
- “Finding Cracker-Altered Files” on page 491
- “Sealing the Crack” on page 498
- “Finding set-UID Programs” on page 499
- “Finding the mstream Trojan” on page 500

## 13.1 Check Your `/var/log` Logs

Many Linux daemons and other important programs (and the kernel) keep a log file of their activities, and you should scan these log files at least daily for signs of a break-in. Scanning techniques were discussed in Part II in detail, including the use of automatic scanners, such as `logcheck`, that will recognize entries resulting from crackers from the thousands of boring routine entries. If your system is on the Internet, you will see cracking attempts at least weekly.

Linux and UNIX have a standard directory where most log files are kept that is either `/var/log` for distributions such as Red Hat, or `/var/adm` for distributions such as Slackware. I always create a symlink from whichever of these exists to the other name so I do not have to worry about this distinction once I set the system up. (I also do this with the mail directory so that I always can get to it via `/usr/mail`, even though typically it will be `/var/spool/mail` on Linux.)

## 13.2 The `syslogd` and `klogd` Daemons

These daemons provide a standard logging mechanism for daemons, other programs, and the kernel with the ability to control how messages are logged and which allow remotely logging to other more secure systems. In Part II you learned how to use them. Here you learn how to interpret the results when you suspect that crackers have been at work.

## 13.3 Remote Logging

The `/etc/syslog.conf` file can accept an action to send the message to another Linux or UNIX system for logging. This feature is why the host name is reflected in all logged messages. To do this, specify an action of an at-sign `@` followed by the remote system’s host name thusly:

```
*.warn;authpriv.notice;auth.notice @secure.pentacorp.com
```

In order for this to work, the destination system where the messages are to be received for logging must allow this. To allow this, the `syslogd` daemon of that system (`secure.pentacorp.com` in this example) must have been invoked with the `-r` flag. Without this `-r` flag, `syslogd` will silently discard the messages to avoid a Denial of Service attack where one could fill up its disk with bogus messages. (IP Chains or a firewall should be used to block UDP port 514 from unauthorized hosts to protect against this attack.) Your `/etc/services` file will need to list UDP port 514 as being the one for the `syslog` service, but this should be default in any Linux distribution.
