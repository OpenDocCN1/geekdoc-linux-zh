
on and what sites it has blocked as a result. It will also show what failed SSH attempts have occurred, what mail relaying attempts have occurred, etc. If a breach has occurred, it may enable you to discover this through the logging of failed attempts by a cracker to elevate her privileges. It makes clever use of pattern matching to recognize ominous errors that have attack, violation, and similar words that indicate errors for major subsystems. Logcheck has a list of phrases to ignore so you will not be worried about the clones attack because you already know about.

While Psionic renamed Logcheck to LogEntry on its Web site, the gzipped toolbar, the name of the script that you run from the root crontab remains logcheck and otherwise is unchanged from earlier versions. In fact, the LogEntry banner by Psionic is identical to the previous one that was offered on the companion CD-ROM of the first edition of this book to last.

While using Logcheck for monitoring client networks, with dozens of systems, and even for the systems on my own network, I have fixed a number of flaws:

1. Even with inactive systems, anyone can expect e-mail almost hourly. Most e-mails will contain only information in the least important of Logcheck's three levels of severity. However, ignore the e-mail and you risk ignoring a major attack. It would be nice if this was indicated in the initial portion of the subject line so it could be seen easily from a browser screen without having to open the message.
2. It would be nice to have the option of directing Logcheck to notify you by e-mail of security violations and attacks, but you still need to dump "unusual activity" into an ordinary e-mail box (separate from your usual mailbox) to check on occasion. Unfortunately, Logcheck cannot send an e-mail to a different address, depending on the highest severity of the errors encountered.
3. Each entry of a severity also appears in each portion of the report that carries less but possibly important warnings. Consequently, I found myself ignoring the Active System Alert section of the e-mail because these items are also in the Security Violations section of the e-mail. Similarly, I rarely continued to the Unusual System Events because mostly this section repeated the security violations.
4. Almost every entry is substantially longer than 80 characters, causing lines to wrap. This makes it very hard to scan the e-mail rapidly for things that concern me, such as attacks to particular IP addresses or ports.
5. Each line contains data that is not important, such as the system name and kernel: Packet log: when it was obvious by the context that this was an IP Chains entry. Also, various TCP flags of infringed "boiled down" common errors such as packet dropping. In this case, your interest would be in the source and destination systems' IP addresses, ports, and protocol. There is always the option to grep in the original log file for the additional fields in the rare case when one is interested.
6. The SysAdmin is expected to remember protocol numbers, such as 6 for TCP, 17 for UDP, and 2 for DDP. While I know these after analyzing network traffic for over a decade, it still takes longer to interpret the raw numbers.
7. Logcheck includes PortSentry's log of what command used to lock out each attacker. I know what I told PortSentry to do, I do not want to see this same long line dozens of times a day.
8. Logcheck does not allow altering the From: line to indicate which computer it came from. If Pentacorp has a firewall in each of, say, eight offices, an e-mail address of root@pentacorp.com is not informative, especially when other e-mail comes from root.

I have corrected these problems in Logcheck and included my enhanced version on the CD-ROM. Alternatively, if you e-mail a request for it to book@verysecurelinux.com, I will provide you with a copy of it. Psionic's original may be obtained by starting at www.psionic.com/products/logsentry.html and following their instructions to do this and "sign" that try to make some builds. The resulting tarball also may be obtained from the CD-ROM under the original name of logcheck-1.1.1.tar.gz. My enhanced version is under the subdirectory as logcheck-1.1.1ibob.tar.gz.

Some typical output follows, with the first item being the date and time in the format MM/DD-HH:MM:SS.

Active System Attack Alerts (dada)
------------------------------------
04/16-16:39:46 portsentry: ATTACK: riddle.com/212.223.7 TCP 80

Security Violations (dada)
--------------------------
05/15-19:42:44 C in DENY e0 T 151.27.1.37:1 126.193.251.197:0 S #21
05/20-03:03:15 T I=e0 126.193.251.187 126.193.251.197 DF ICMP=8:0
05/21-00:21:51 T D I=e1 O=e0 230.83.97.1944 76.121.32.45-6346 TCP

The System Attack was generated when PortSentry detected the riddle.com scanning our system for a Web server (probably did only to TFS). The fact that we are not running a Web server on the firewall system caused PortSentry to consider this attack and locked riddle.com out. (Specifically, PortSentry determined this by seeing a packet sent to a port where no service was listening). The line beginning with C is what IP chains looks like. This packet was on the input chain. The e indicates that the packet came in eth0, and the T indicates that the protocol is TCP. The source and destination IPs and ports are not enhanced, followed by s to indicate that the SYN bit was set (TCP protocol only). Lastly, the #21 indicates that this number 21 in the input chain.

The second violation, starting with T, indicates an IP log entry. Normally you will not see both IP Tables and IP Chains on the same system (as only the IP Table or the IP Module may be running at any particular time, and most people use the other). The I= would be the input interface if applicable. The O=e is short for OUT=eth0. Next are the source and destination IPs. The DF was set by the Division of Mysteries.³ Lastly, the ICMP type=8 indicates that this is an ICMP message of type 8 (ping) and subtitle 0 (there are no other ping subtypes).

The violation is another IP Tables entry line but was generated from rules generated by SuSE's firewall2 script, available on recent SuSE releases. The initial D (DEFAULT) is my shortened form of SuSE's verbose SUSE-FW-DROP-DEFAULT.⁴ I know that it is an SuSE system, this is a firewall message, and probably it would be logged if it was not being dropped. Therefore, I use T (for IP Tables) to indicate all of this. Realistically, one learns to read these very quickly and these shortened forms can be read much faster than muddling through the wrapped-line output from IP Tables or IP Chains. This is the opinion of my Beta testers.

Let us now walk through an installation. First, ensure that syslog is running; it should be running on any Linux system or BSD-like Unix system. The log files probably will be in /var/log, with the messages file generating a copy of all messages except debugging and mail logs. It is recommended to fix the permissions of all log files changed to 600 and bound to stop crackers from using ordinary accounts to get information from them. Next, use the CD-ROM as /mnt/cdrom and issue the commands:

```
zcat /mnt/cdrom/book/logcheck-1.1.lob.tar.gz | tar -xof -
logcheck-1.1.lob
```

Now, read the text files LICENSE, CREDITS, and crontab. For those who use Sendmail, edit /etc/mail/aliases and create an alias for the e-mail of whoever should be notified of security problems. Preferably, this should be a separate mailbox for your regular mailbox to avoid cross-contamination. Then, create an alias, alertpage, for e-mail-capable pages to receive security violation and attack e-mail. If no pager e-mail is desired,

```
alertpage:/dev/null
```

Now update the database with

```
newaliases
```

³ DF means that the Dont Fragment flag was set. It took me using grep on the kernel source tree to figure this out as it is not documented.

⁴ Under IP Tables, you can specify that certain text should be prepended to the log file that is generated: SuSE's firewall2 script, standard on recent releases, prepends SUSE-FW-stuff, which makes for lines with repetitive text. That is, the varying part of a space-separate word of an error message should be at the beginning of the word (and at the beginning of the line) or it will likely not be detected.

There is a good lesson here for writing error messages for human consumption, including log messages (applicable to firewall2, PortSentry, etc.). Work hard not to include obvious, repetitive, or irrelevant information in error messages. This unnecessary information serves mostly to make understanding the error message more difficult. This puts the intended reader of the message at risk for not understanding its critical information. Also, processed log messages should not exceed 80 characters, to avoid line wrapping. By following this lesson, the person reading the messages can skim lines of interest far more quickly and spend time reading unnecessary words.
