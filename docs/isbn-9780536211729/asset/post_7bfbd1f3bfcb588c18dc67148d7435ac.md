
Large open lists can end up in the Realtime Blackhole List and that is very bad. This is because many of the list recipients' Sendmail configurations will reject any e-mail from that list and it is hard to get out of the Blackhole.

The Sendmail alias capability (when a name expands to more than one recipient) is an example of an open list. Majordomo can be configured so that lists are closed. A closed list only accepts e-mail from someone on a list of senders. Commonly, this list of allowed senders is the list of recipients, for unmoderated lists. GNU Mailman is another popular mailing manager.

### 3.2.12 Sendmail DoS by Filling the Disk

An attacker can create a DoS attack by sending so much e-mail that the system's disk is filled up. One of the main benefits of keeping some of the files that can "grow" without user input under /var is that this allows /var to be a separate file system. By having it be a separate file system, if /var runs out of space it will not affect the operation of the rest of the system.

The reason for /var is that /var is short for variable. Besides /tmp and /home, it is the only part of the system that could be mounted read-only and shared across diskless workstations. /usr/tmp is a symbolic link to /var/tmp.

This was popular back in the Sun days when disks were expensive and the more parts of the systems that were the same, the less maintenance burden there was. Microsoft has put some of this concept into practice in Windows 2000. With embedded Linux becoming popular, it is again becoming popular.

A better solution is to impose quotas under the /var file system. Thus, each user could be limited to a reasonable amount of e-mail. An even better solution is to put a quota on the mail group. Because the mail group is only used for e-mail then a mail quota will work regardless of whether /var is a separate partition. Recall that the quota set for a user or group is a per-file system value.

The following command will list the amount of space each mailbox is using, with the largest mailboxes listed first.

```
ls -ss /var/spool/mail
```

The following command lists the largest 20 mailboxes and mails the result to root. It is suitable for use in root's crontab.

```
ls -ss /var/spool/mail | head -20 | /bin/Mail -s mailboxes root
```

## 3.3 Telnet

Telnet has two problems. All of a user's data is sent unencrypted so that anyone sniffing the network anywhere between your system and the other system will see all the data. It is also vulnerable to a "Man-in-the-middle attack."

The worse is that the password used to log in to the server is in clear text. Assume that the V.P. of Finance downloaded an archive of jokes. A cracker could have sniffed his password. He now might be in the V.P.'s account, reading his confidential files containing bank account numbers, the planned IPO (Initial Public Offering), and details on that great new idea that could make the company millions of dollars.

An additional problem is that a cracker can try guessing each user's telnet password as many times as he wants because telnet does not track the number of incorrect guesses. These bad guesses will end up in the log files. See "An Example for Automatic Paging" on page 358 for a description of how to be notified as soon as someone enters a bad telnet password.

Moreover, telnet uses the user's login password if shadow passwords are not being used and a cracker gets a copy of /etc/passwd, then the cracker can crack the password on his own system and use telnet without the delay and risk of discovery of repeatedly sending password guesses to your system.

A proper solution is to require your users to use SSH for data that leaves protected networks and to enforce this by configuring the firewall to block telnet's port in each direction. Requiring people to use SSH instead of telnet internally will also protect against crackers, including any inside the organization, getting into your internal network and sniffing internal data from there. Removing telnet and telnetd will help here. Another option is using stelnet, an SSL-wrapped telnet solution.

## 3.4 FTP

FTP suffers from most of the same problems as telnet and the solution is the same. Replace it with SSH (for most nonanonymous use). SSH2 offers sftp, a protocol introduced early in 2000. Because some sites will not want to use SSH2 due to its license being more restrictive than SSH1 or OpenSSH, alternatives are SSH-wrapped FTP, scp, and SSL-wrapped ftp. OpenSSH now offers sftp too.

Additionally, even some recent versions of WU-FTPD, the FTP daemon created by Washington University at St. Louis, suffer from security bugs. These include a buffer overflow bug that allows a remote intruder to make himself root. This version was common in distributions as late as 1999.

> I determined that one of my client's development machines very likely was broken into via this overflow bug.

I scanned his system for cracker-induced alterations using methods discussed in Part IV, using tar. The Network Administrators and I then explained to him the benefits and usage of TCP Wrappers and SSH and how they could allow him safely to connect from his home system and to transfer files between these two systems.

You will want to check the errata for your distribution, discussed in Appendix A, to ensure your version of WU-FTPD does not have these bugs in it. The Linux Administrators Security Guide reports that several nasty DoS vulnerabilities still exist in WU-FTPD as of 1999 and that improper server setup allows a cracker to obtain privileges he should not have. "Upgrade WU-FTPD" on page 106 tells where to get updates and the most recent version available.

ProFTPD is preferred by many security-conscious sites, including Debian and SourceForge, some Linux vendors. It may be downloaded from

```
www.proftpd.net/
```

Another alternative is to make use of the BSD FTPD implementation, which has been ported to Linux. It is available from the CD-ROM or from

```
ftp://quadramaran.ens.fr/pub/madore/ftpd-BSD/
ftpd-BSD-latest.tar.gz
```

or

```
ftp://quadramaran.ens.fr/pub/madore/ftpd-BSD/
ftpd-BSD-0.3.2-1386.rpm
```

A popular thing for crackers to do when they compromise a system's FTP daemon or if they find a site that allows them to upload data for public download is to use it as a repository for warez (cracker-speak for cracker wares; in other words, cracker programs for distribution that might get you accused of being a cracker) and pornography which could make for some really bad publicity. The storage of music and other copyrighted material is becoming common too. IRC 'bots are also a popular usage. This is a very good reason not to offer a public FTP site.

There are a number of solutions including some combination of the following:

- 1. Wrap the FTP daemon with SSH or use sftpd, that is part of SSH2. See "TCP Wrappers" on page 109.
- 2. Allow the use of FTP only by trusted clients via TCP Wrappers or firewalling with IP Chains.
- 3. Make use of the WU-FTPD feature to chroot anonymous users and even nonanonymous users if desired. Using man 5 ftppass will generate useful documentation on many of WU-FTPD's capabilities to limit which systems and users may access it, how to use its chroot capability, and to specify which commands will be allowed, and so on.
- 4. Consolidate "anonymous FTP" needs onto a single system that has no confidential data and is outside your corporate network, and typically in the DMZ. Thus, if it is cracked then there is nothing to "get," though there will be a cracker causing the distribution of undesirable files.
- 5. On your Web server (http), supply the MD5 checksums for the files that you distribute on your FTP server so that those downloaded files can verify that they are correct and that the files on the FTP server have not been altered. For extra security, CGI operation should place a proxy on a third machine and all of these machines should be in a DMZ that allows appropriate services to each of these.
- 6. If one person wants to give data to a second person and they cannot transfer it easily via other methods as e-mail (possibly wrapped in PGP or SSL), the first person could FTP up to the FTP server and then the second person could pull down. The advantage of this two-step procedure over one ftping into the other user's machine is that neither user's system has to suffer the security risks of being an FTP server.

As part of the "Rings of Security," you do not want to allow anyone to FTP into your root account because knowing only the root password would crack your system. Likewise, you will want to block FTP from accessing your other system accounts and create additional accounts too. These account names may be listed in the /etc/ftpusers file, one line per account, to prevent anyone from logging in via FTP to them. Blank lines and comment lines starting with the "#" character are allowed too.

The most elegant and easiest way to add a user to the /etc/ftpusers to forbid any remote user from logging into FTP as this user is the use of the echo command and the shell >> operator to append a command's output to the named file. Thus, to prevent using the root and ftp (anonymous) accounts via FTP, follow the following commands. (Thanks to the Neuss team for this technique.)

```
echo root >> /etc/ftpusers
echo ftp >> /etc/ftpusers
```
