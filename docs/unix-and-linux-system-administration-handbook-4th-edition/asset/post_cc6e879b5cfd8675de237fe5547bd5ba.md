
You cannot design a mail system in a vacuum. You must be synchronized with (or at least not be in conflict with) your DNS MX records and your firewall policy.

## Queue monitoring

You can use the **mailq** command (which is equivalent to **sendmail -bp**) to view the status of queued messages. Messages are queued while they are being delivered or when delivery has been attempted but has failed.

**mailq** prints a human-readable summary of the files in **/var/spool/mqueue** at any given moment. The output is useful for determining why a message may have been delayed. If it appears that a mail backlog is developing, you can monitor the status of **sendmail**’s attempts to clear the jam.

There are two default queues: one for messages received on port 25 and another for messages received on port 587 (the client submission queue). You can invoke **mailq -Ac** to see the client queue.

Here is some typical output from **mailq**. This case shows three messages waiting to be delivered:

```
$ sudo mailq
/var/spool/mqueue (3 requests)
-----Q-ID----- --Size-- -----Q-Time----- ------------Sender/Recipient------------
k623g-YK008732 23217 Sat Jul 1 21:42 MAILER-DAEMON
                  8BITMIME (Deferred: Connection refused by agribusisonline.com.)
                                      <NItmz@agribusisonline.com>
k5ULkAHB032374 279 Fri Jun 30 15:46 <randy@atrust.com>
                  (Deferred: Name server: k2wireless.com: host name lookup failed)
                                      <rIder@k2wireless.com>
k5UJDm72023576 2485 Fri Jun 30 13:13 MAILER-DAEMON
                  (reply: read error from mx4.level3.com.)
                                      <Ifnist@bnplanet.com>
```

If you think you understand the situation better than **sendmail** or you just want **sendmail** to try to redeliver the queued messages immediately, you can force a queue run with **sendmail -q**. If you use **sendmail -q -v**, **sendmail** shows the play-by-play results of each delivery attempt, information that is often useful for debugging. Left to its own devices, **sendmail** retries delivery every queue run interval (typically every 30 minutes).

## Logging

**sendmail** uses syslog to log error and status messages with the syslog facility “mail” and levels “debug” through “crit”; messages are tagged with the string “sendmail.” You can override the logging string “sendmail” with the **-L** command-line option; this capability is handy if you are debugging one copy of **sendmail** while other copies are doing regular email chores.

> See Chapter 11 for more information about syslog.

The confLOG_LEVEL option, specified on the command line or in the config file, determines the severity level that sendmail uses as a threshold for logging. High values of the log level imply low severity levels and cause more info to be logged.
Table 20.17 gives an approximate mapping between sendmail log levels and syslog log severity levels.

## Table 20.17 sendmail log levels vs. syslog levels

| L | Syslog levels | L | Syslog levels |
|---|---|---|---|
| 0 | No logging | 4 | notice |
| 1 | alert or crit | 5~11 | info |
| 2 | crit | ≥12 | debug |
| 3 | err or warning |  |  |

Recall that a message logged to syslog at a particular level is reported to that level and all those above it. The /etc/syslog.conf file determines the eventual destination of each message. Table 20.18 shows their default locations:

## Table 20.18 Vendor's sendmail logging locations

| System | Log file location |
|---|---|
| Ubuntu | /var/log/mail.log |
| SUSE | /var/log/mail |
| Red Hat | /var/log/maillog |
| Solaris | /var/log/syslog and /var/adm/messages |
| HP-UX | /var/adm/syslog/mail.log |
| AIX | /var/log/mail |

Several programs can summarize sendmail log files, with the end products ranging from simple counts and text tables (mreport) to fancy web pages (Yasma). You might need to—or want to—limit access to this data or at least inform your users that you are collecting it. Yasma (Yet Another Sendmail Log Analyzer), for example, lets you hide the username part of email addresses in its reports.

## 20.14 Exim

The Exim mail transport and submission agent was written in 1995 by Philip Hazel of the University of Cambridge and is distributed under the GNU General Public License. The current release, Exim version 4.71, came out in late 2009.

16. Wouldn't it be nice if standardization efforts could sort out some of these random and apparently meaningless differences so our scripts could be more portable?
