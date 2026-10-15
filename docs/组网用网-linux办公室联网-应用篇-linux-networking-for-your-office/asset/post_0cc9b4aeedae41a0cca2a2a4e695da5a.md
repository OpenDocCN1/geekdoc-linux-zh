
- Product Web sites—You can check the Web sites for major packages, such as Samba, for security-related updates. It’s particularly important that you check such sites routinely if the package in question isn’t part of a standard installation of your Linux distribution, such as xinetd.
- The comp.security newsgroup hierarchy—There are several Usenet newsgroups with names beginning comp.security. These groups can be an important source of information on computer security issues.
- Mailing lists—There are numerous security-related mailing lists, mostly concerned with fairly specific topics. If you’re interested in locating a mailing list related to a specific topic, try starting at an appropriate Web site and skim for information on mailing lists. You could also try posting a query for information on an appropriate newsgroup. Both CERT and CIAC maintain mailing lists. To subscribe to the former, send a message to cert-advisory-request@cert.org with a Subject line of subscribe. To subscribe to the CIAC mailing list, send a message to majordomo@tholia.llnl.gov with subscribe ciac-bulletin as the text of the message.

In addition, there are a plethora of security-related Web sites, including sites concerned with the security of specific products and protocols. Any Web search engine should turn up sites on specific topics in which you’re interested.

## Summary

Keeping your system from being used or abused by unauthorized individuals is a difficult task, and there’s no way to be 100% secure. Even if you had extraordinary knowledge of computer security, you could become the victim of a bug in a program you trust, such as inetd, xinetd, sendmail, or some other server, or even potentially of a client program. For this reason, you should monitor Web sites and other online resources for security update information.

You should close down services that aren’t needed on specific interfaces or by sites other than those that do need them. If your FTP server, to name one example, is online only so that your colleagues at a specific institution can exchange data with you, you can use TCP Wrappers, xinetd, or ipchains to block that server to everybody but your colleagues.

You should pay attention to passwords, as well, even when you believe those passwords are only usable on your internal network. Passwords are your first and, sometimes, last line of defense against crackers. Because a Linux server is likely to have many users, it’s also likely to have many passwords, and this fact means that your users need to understand the importance of password security, more so than they need to understand the workings of inetd or similar administrative details.

Finally, all the network security measures conceivable will do you no good if your computer is stolen, destroyed, or even just physically accessible to a cracker for a time. You should take measures to keep unauthorized personnel away from the computer, and you should also perform regular backups and store some of them off-site.

## INDEX

# (pound signs)
afp config files, 300
/etc/inetd.conf files, 65
NFS map files, 250
% (percent signs),
/etc/smb.conf file variables (Samba), 263-264
& (ampersands), forking
afp parameters, 304
/etc/exports file, NFS, 244
* (asterisks),
/etc/exports file (NFS), 244
\ (backslash characters)
directory name separation (DOS, Windows and OS/2), 218
/etc/smb.conf configuration (Samba), 268
versus slashes (/), 285
: (colons) (MacOS), 218
= (equal signs),
/etc/smb.conf file (Samba), 263
AppleVolumes (Netatalk), 300
? (question marks),
/etc/exports file (NFS), 244
/ (slash characters)
versus backslashes (\), 285
directory name separation, 218
100base-T,
hubs/switches, 10, 20-25
10base-2, 10
10base-5, 10

10base-T, 10
hubs/switches, 20-24
3COM
3c59x, chipset, 19
EtherLink XL, 528
4Front Technologies
Web site, 529
8.3-style filenames, conversion, 231
absolute links, 221-222. See also links
access. See also security
/etc/exports file options, NFS, 245
NFS permissions
remote and local users, 248-249
root, superusers, 251
user map files, 250-251
printers
/etc/hosts.equiv, 381-382
/etc/hosts.lpd, 381
controlling, 382-383
Samba, 395-397
remote
applications, 426-428
configuring (Macintosh), 411-415
intranets, 427
login, 431-438
security, 438-442
sites, 427-428
terminal sessions, 428-434
Remote X, 444
Samba options, 268-269
troubleshooting (Samba), 281

VNC, 454-459
Macintosh, 456-457
MacOS, 458-459
starting, 455-456
Windows, 456-459
X server, 445-454
applications, 445-447
login, 449-453
performance (applications), 453-454
security, 460
starting applications, 453
terminals, 449
Account Information dialog box, 201
accounts
PPP, 186-187
text-mode tools, 134-135
user
configuring, 131-137
linuxconf, 132-134
activating interfaces, 169-170
adapters (SCSI), 525
Add a Printer Entry dialog box, 403
adding
features, 141
parallel ports, 530
Address Resolution Protocol. See ARP
addresses
Ethernet, 17
fixed
activating interfaces, 169-170
configuring, 166-179
DNS servers, 173-179
/etc/hosts file, 168-169
