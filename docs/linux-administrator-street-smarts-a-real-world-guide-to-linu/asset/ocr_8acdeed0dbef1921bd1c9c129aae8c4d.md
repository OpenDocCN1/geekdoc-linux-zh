may need to edit twpol.txt to eliminate references to files that you don't have on your system and to add information on files that you do have but that the default file doesn't reference. Use the twin $t$ al . $s h$ program (which often resides in /etc/tripwire) to generate the binary configuration files and other critical database files. This utility will ask you to set a pair of passwords, which are like passwords but are typically longer, to control access to the Tripwire utilities. You'll then need to enter these passphrases to have the utility do its encoding work.  

Once you've generated the basic setup files, type tripwire --init to have Tripwire generate initial checksums and hashes on all the files it's configured to monitor. This process is likely to take a few minutes. Thereafter, typing tripwire --check will check the current state of the system against the database, and typing tripwire --update will update the database (say, in case you upgrade a package). The --init and --update operations require you to enter the passphrase, but --check doesn't. Therefore, you can include an automated Tripwire check in a cron job. (Phase 3 describes cron jobs in more detail.)

> **NOTE**  
> Tripwire is best installed and initialized on a completely fresh system, before connecting the computer to the Internet but after all programs have been configured. Although it's possible to install it on a system that's been up and running for some time, if that computer has already been compromised without your knowledge, Tripwire won't detect that fact.

# Using chkr00tkit

The chkr00tkit program (http://www.chkr00tkit.org) is something of a last-resort method of detecting intrusion and is the closest thing in the Linux world to Windows virus scanners. (Linux virus scanning programs also exist, but they're intended mainly to check for Windows viruses on Samba shares. Linux viruses are not a problem in the real world, at least not as of late 2006.)  

Many crackers use root kits, which are prepackaged intrusion tools. When an intruder runs a root kit against a target, the root kit software probes for known weaknesses (such as servers with known security bugs), breaks in, and installs software to enable simpler access by the intruder. The intruder can then log in using Telnet, SSH, or the like and gain full control of the system.

> **NOTE**  
> Intruders who use root kits are often referred to as script kiddies. These miscreants have minimal skill; they rely on the root kit to do the real work of the intrusion. Some people prefer to reserve the term cracker for more skilled intruders, but others consider script kiddies to be crackers with minimal expertise.

Using chkr00tkit is fairly straightforward: Type its name. The result is a series of lines summarizing checks that the software performs. These lines should all end with not infected, no suspect files found, or a similar reassuring message. If any message alerts you to an intrusion, you should take immediate corrective measures.