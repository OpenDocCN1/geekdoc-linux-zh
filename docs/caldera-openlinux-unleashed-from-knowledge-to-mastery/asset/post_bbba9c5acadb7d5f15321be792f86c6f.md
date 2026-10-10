
- Use non-routable (private) addresses for machines on the local network. Drop all packets coming from the Internet destined for (or claiming to come from) non-routable addresses. Use masquerading to allow internal machines to access the Internet.

- Have all firewall rules log hits. The log should be done on the firewall machine as well as on a logging host on the internal network.

For the ultimate in firewall security, you could set up a firewall something like this:

- Use a machine with no hard drive.
- Create a write-protected bootable Linux floppy that contains the kernel and a minimal file system.
- When the firewall boots from the floppy, it should create a RAM disk and use that as a root partition. Once the system has booted, configured all interfaces and set up the firewall rules, delete the sh, route, and ifconfig binaries. (In fact, delete all system binaries—they are not needed once the system is up and running.) Because the binaries are in a RAM disk, the bootable floppy is unaffected.

The beauty of this setup is that the lack of even sh makes it very difficult for an attacker to take control of the firewall. Even if he does somehow manage to get a shell, the attacker cannot permanently modify the firewall setup (which is on a write-protected floppy).

The mechanics of this kind of firewall setup are a bit involved; a starting point is the “Initial RAMDisk” article in /usr/src/linux/Documentation/initrd.txt. Of course, you need a second machine for testing purposes until you have the setup just right.

## A Firewall Is Not a Panacea

A firewall prevents certain packets from the Internet from entering your LAN and certain packets from your LAN from entering the Internet. That is all. If you are running a Web browser with an exploitable buffer overrun from behind your firewall, the firewall cannot prevent a buffer overrun attack. For this reason, you need to practice deep security. Make all of your LAN workstations secure enough that you’d feel confident putting them on the Internet even without a firewall. Then put in a firewall anyway.

Each LAN machine (if it is running Linux) should have its own firewall rules to reject packets from outside machines. For example, no outside machine should attempt to access any UNIX services on internal machines, so all packets not coming from the local network destined for ports below 1024 should be blocked.

In particular, internal machines should not trust the firewall. The firewall will be the first machine compromised by an attacker; internal machines should not allow connections originating from the firewall machine.

Although it may be overkill, you can use the TCP Wrappers facility as well as firewall rules to restrict access to TCP services. For an overview of the facility, see manual pages `hosts_access(5)`. On modem computers, the overhead introduced by multiple levels of access control is acceptable.

### SUID/SGID Programs

Get a list of every SUID or SGID program on your system and make sure you understand why it needs to be SUID or SGID. In many cases, such programs can run quite well without special privileges. If you are unhappy with a SUID program, remove it or turn off the SUID bit.

For example, on my system, the file /usr/bin/ponisdn is installed in SUID root. Since this command is for monitoring the ISDN subsystem and I do not have any ISDN hardware, it is better to remove the program (or at least turn off the SUID bit) than leave it around for a potential exploit.

### Keeping Up-to-Date

You should periodically check your vendor's Web site for security updates. Security problems and fixes happen with startling frequency; if you are serious about security, you'll try to keep on top of them. An excellent resource is the BUGTRAQ list at `http://www.securityfocus.com`. This is a full-disclosure list (it will tell you exactly how to exploit bugs). Since computer criminals most likely read the list, you'd better read it too, to stay ahead (or at least abreast) of them.

Be careful, however: Usually it's a good idea to update software when new versions are released, but sometimes new versions introduce new bugs or security holes.

Unless you know for certain that a release fixes a critical security problem, I would evaluate each upgrade and wait before updating. The brave souls who upgrade first will report their experiences soon enough if new security bugs are found.

### Monitoring, Detection, and Logging

Monitoring and logging tools are essential parts of overall security. They can alert you to attack attempts before an attacker gains entry to your system. They can also help you trace attackers who compromise your system (providing logs are set up so that attackers cannot destroy them).

### System Logs

Most logging on Linux is done with the syslog facility. A file called /etc/syslog.conf controls how and where information is logged. This information was covered earlier; for more details, see syslog.conf(5) and syslogd(8).

For maximum security, you should log messages to the local host and to a central logging host. For ultimate security, pass the log output to a line printer. It is much easier for an attacker who has gained root access to delete disk files than to destroy pieces of paper in a locked room hundreds of miles away.

### Log Analysis

System logs typically contain quite a bit of information, most of which is boring and routine. This is dangerous, because it can cause you to skip over log entries that should alert you to problems.

There are several log analysis tools available, but (unfortunately) none is included with Caldera OpenLinux 2.3.

One of my favorite log analysis tools is swatch, available from ftp://ftp.stanford.edu/general/security-tools/swatch. This is a Perl script that lets you specify which log entries you are not interested in (using regular expressions). The tool scans the log files, discards uninteresting messages, and mails you the rest.

Specifying uninteresting messages is safer than specifying which messages you want, because an unanticipated message type might crop up and be discarded.

You should run swatch on your log files daily and spend 5–10 minutes reading the output every day.

### Typical Signs of Attacks

What log entries might indicate attack attempts? Look for these entries and treat them as suspicious:

- Many failed login attempts. These could indicate password cracking attempts. However, do not overreact—a legitimate user may have forgotten her password.
- Many failed (or successful!) su attempts. Again, a few failed attempts might be accidental (typing du instead of su, for example).
- Accesses to many different network services. If something is connecting to your mail agent, FTP server, Web server, or Telnet client often and in quick succession, your machine is likely being port scanned. In this process, an attacker tries connecting to many different ports on your machine to determine which services are running. Some attack scripts even read banners returned by the various service daemons, determine which security holes they contain (if any), and automatically compromise them.
- Any strange or persistent failure messages. These could be caused by hardware or software problems—or by an attacker probing your setup.

Please note that the system logger itself can be used in a denial of service attack. The system log daemon syslogd has an option (-r) that lets it receive logging messages over the network. An attacker can send thousands of spurious logging messages to the system logger, filling the disk space on the logging machine. You should normally disable the -r option or use firewalling rules to control which machines can send logging messages to the logging daemon.

## Monitoring Files

If an attacker gains control of your system, he typically modifies some files to leave a backdoor for later access. You can prevent such actions by making it hard to modify files, or you can detect them by using monitoring tools.

### Prevention of File Modification

The only sure way to prevent file modification is to mount files from a read-only device such as a CD-ROM. Note that mounting a normal hard disk as read-only is not secure, because an attacker who gains root access can easily remount the disk as read-write.

> **Note**
> You may be able to make hardware modifications that render the disk drive truly read-only. A simple switch on the write line of the disk cable could do the trick. However, I am unaware of any disk hardware that actually implements this. If you are handy with a soldering iron and brave enough, you could cut the write line on your disk cable and insert a switch. But don’t do this unless you absolutely know what you are doing.

Mounting large parts of the file system as read-only is tricky, but it can be done. In principle, the root partition should be mountable as read-only. The only directory trees that actually need write access are

- /var Contains runtime modifiable data
- /tmp Contains temporary files
- /home Contains users’ home directories

You can place these three trees on a hard disk and the rest of the system on read-only media.
