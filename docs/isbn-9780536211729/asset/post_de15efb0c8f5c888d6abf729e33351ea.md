
you might assume that a cracker was guessing account numbers, and you will want to lock his system out via TCP Wrappers or the other techniques discussed.

> If logging mistyped login names is such a great idea, how 'bout logging mistyped passwords? This would allow SysAdmins to see if a password merely was mistyped or was being guessed at. This was tried at Berkeley around 1978 by the SysAdmins, including Bill Joy.

Their “clever” idea failed to account for the fact that the gray hats that they were trying to catch had root access via another method, but did not know the root password. After a day's worth of typos when the SysAdmins tried to log in, it was clear what the real password was. Consider what password these typos indicate:

secret
scret
sercet
seecret
secre

An involved solution to this problem might be to use a secure encryption method built into login to store or transmit encrypted forms of the mistyped passwords. GPG's filter capability could be used.

**sendmail** entries show remote systems connecting to your **sendmail**, possibly to exploit security holes in all but the latest **sendmail** programs or to bounce spam off your system by relaying it.

**syslogd** entries show **syslogd** exiting (typically via the Terminate signal, signal 15) which might be a cracker stopping **syslogd** so that it does not log his actions. (If the cracker is smart he will use a Kill signal, signal 9, which will not give **syslogd** a chance to log the event.) Another **syslogd** entry would be it starting up, possibly by a cracker after he has done his dastardly deeds. Routine entries would be when **syslogd** gets restarted by **logrotate** to start using new log files, which should raise your concern.

**init** entries are made by **init**, the initial nonkernel process created on boot up that forks all other processes on the system. The usual entries would be the system switching states, with state S being single-user, state 3 being the normal multi-user state with networking enabled, state 2 being multi-user without networking (not used much for Linux), and state 6 meaning rebooting. **Init** entries do not show **init**’s PID in square brackets because **init** always is PID 1.

**named** entries are made by **named**, the DNS daemon. Typical entries would be for **named** starting, updating its zone information, and rejected requests.

**lpd** entries show errors encountered by the Line Printer Daemon; these show incorrect configuration or possible exploits.

**dhcpd** entries are from the Dynamic Host Configuration Program Daemon that allows a central server to specify the INET (IP) address that your system should use. These “leases” expire periodically and must be renewed. There may be exploits here.

**last message repeated** entries are used when a message occurs a number of times in succession, to indicate how many times it has been repeated to avoid many lines of log file entries for a repeated event, such as being out of memory or encountering bad disk sectors.

### 13.4.3 syslog

Unlike the messages log file, syslog only logs “problems” and so should be looked at more carefully. Typical problems would be login noting bad passwords when logging in (that also could indicate invalid account names), failed attempts to su, sendmail problems, syslogd conditions (which could indicate cracker activity), and in.telnecd refusing access.

### 13.4.4 kernlog

Not all Linux distributions ship an /etc/syslog.conf file configured to log kernel messages. You certainly want to ensure that yours has a line similar to

```
kern.* /var/log/kernlog
```

This will log kernel messages of all priority to the /var/log/kernlog file. This file will log things such as doing floppy I/O after a floppy change, device drivers being loaded while the system is loaded, system reboots, and attempts to write to a floppy set Read/Only. Although these all could be normal operations, they also could be the work of crackers if no authorized person did them.

Some of these messages are self-explanatory and are listed here. (All of these lines start with the date; some lines are wrapped to fit on the page.)

```
Dec 9 15:10:34 cavu kernel: floppy0: Drive is write protected
Dec 9 15:10:34 cavu kernel: end_request: I/O error, dev 02:00, sector 0
Dec 15 11:16:15 cavu kernel: loading device 'eth0'...
Dec 15 11:16:15 cavu kernel: eth0: Bog us2000, port 0x360, irq 7,
     Auto port, hw_addr 28:44:29:31:0A:69
Dec 15 11:16:31 cavu kernel: eth0: autodetected 10baseT
Dec 17 20:27:25 cavu kernel: VFS: Disk change detected on device 02:00
```

### 13.4.5 cron

This file logs each command that the cron daemon, `crond`, forks, preceded by the user, time, and PID, and action of the forked process. An action of CMD is the normal case of cron forking a scheduled process. An action of REPLACE is the logging of that user updating her cron tab that lists the schedule of tasks to execute periodically. An action of RELOAD, shortly after a REPLACE, means that cron noticed a user's crontab has been updated and that cron needed to reload it into memory. You will want to look for anything out of the ordinary.

### 13.4.6 xferlog

The `xferlog` file is a log of FTP transfers that may show what files the cracker copied onto or off of your system. These files will show the weapons he brought onto your system to hurt you and what files of yours he copied for his use.

The first space-separated field is the date and time, the following fields show how many seconds it took to copy the file, the remote system, the size of the file, the local pathname, transfer type (a for ASCII or b for binary), flags relating to compression or use of `tar` (or `_` if none), direction (i for incoming or o for outgoing, with respect to your system), access mode (a for anonymous, g for passworded guest, or r for a real user), user name, service name (usually ftp), authentication method (1 for RFC 931¹ or 0), and authenticated user ID (or *). Note that FTP is one of many ways to move files between systems.

### 13.4.7 daemon

This file, not present on all Linux systems, logs activities by daemons not otherwise discussed. Of these, one would be `cardmgr` that manages PCMCIA removable cards for laptops.

### 13.4.8 mail

This file, sometimes called `maillog`, contains an entry for each piece of e-mail sent into or out of the system. The principal security use would be to see what systems the cracker might have used to send cracking tools in from or to send your data out to.

It also will show what addresses actually were used for spammers; this can help you block their future attempts. There seem to be large volumes of spam from various top-level domains allocated to various countries that you probably do not exchange a lot of e-mail with, such as Russia and other Eastern Bloc nations and various islands. Although you could track this for a while and then block these domains to reduce e-mail, a much better solution is offered in "Blocking Spam" on page 133.

¹ RFC 931 is available at www.faqs.org/rfcs/rfc931.html

This log file is easy to interpret. If your system is using a “relay” system that actually sends the e-mail to the destination, this will be noted in the log. Similarly, attempts that fail, usually temporarily, due to a system being down are noted. The times of successful and delayed e-mail are clues to the cracker’s hours of operation. Also, e-mail sent out from accounts that are not for real users (such as bin) or from accounts of people on vacation, no longer with the company, etc., will be from crackers unless automatic programs have generated it. Examples of the latter are “vacation” bots, cron jobs, and calendar.

A second security problem to look for in the mail log file is the use of your system as a “mail relay,” usually by spammers. I refer to this as “drop-shipping spam.” This means sending e-mail to your system (by connecting to your port 25 where you probably have sendmail listening) with a destination address other than your system and other than systems that you intentionally relay mail for.

If you leave your system open to this, it is likely that a spammer will discover this and send spam that appears to the world to originate from your system. This is because the standard sendmail does not always give indication to the recipient of where the e-mail came from because this is the job of the sending system’s mail software.

The spammer does this by specifying your hostname as a “smart relay” in his /etc/sendmail.cf file or Windows-based spamware. This generates e-mail that requests that your sendmail then forward his e-mail to his final victims. This e-mail will show your system as the originator of the spam, not his. Most recent distributions are set up by default to block mail relaying. You should verify this, as was discussed in “Drop-Shipping Spam (Relaying Spam)” on page 133.

The consequence of this is that your system will suffer the load of sending all of the spam (because each of his e-mail messages to your system can request dozens or hundreds of recipients) and will get your system treated as a spammer’s system. This will cause many sites to block any e-mail from your system as a spam site.

There are several sites on the Internet that generate lists of sites where spam originates from and sends these lists out automatically (for free) to the many subscribing sites, which then block e-mail from these addresses automatically. If someone spams through your site, you will find your legitimate outgoing e-mail blocked; it is very hard to get your site off of these lists (or the spammers would plead ignorance and innocence too).

An additional problem, particularly if you are a large site, is that you will get a bad reputation for spamming and sites and people individually will block your e-mail, not visit your Web sites or business, etc.

Using a reasonably modern version of sendmail, such as 8.8.7, the log message for blocked relay attempts will look like the following:

```
Dec 15 08:04:57 cavu sendmail[12657]: IAA12657: ruleset=check_rcpt, arg1=<test@keyyoung.com.hk>, relay=IDENT:administrator[202.82.80.136], reject=551 we do not relay
```
