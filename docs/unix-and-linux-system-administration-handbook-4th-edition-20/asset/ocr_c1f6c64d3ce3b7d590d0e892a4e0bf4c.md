# Chapter 22 Security

time ago. The program said it would draw a picture of a turkey on your terminal screen, but it actually deleted files from your home directory.

Trojan fragments appear in major software packages now and then sendmail, tcpdump, OpenSSH, and InterBase have all issued advisories regarding malicious software in their products. These Trojans typically embedded code that allows attackers to access the victim's systems at all. Fortunately, most vendors fix the software and issue an advisory in a week or two. Be sure to watch the security mailing lists for any network software packages you run on your hosts.

Even given the number of security-related escapades the UNIX community has seen over the last few years, it is remarkable how few Trojan incidents have occurred. Credit for this state of affairs is largely due to the speed of Internet communication. Obvious security problems tend to be discovered quickly and widely discussed. Malicious packages don't stay for long on well-known servers.

You can be certain that any software that has been discovered to be malicious will cause a stink on the Internet. Google the name of a software package before installing it and make sure the first page of results doesn't look incriminating.

# Rootkits

The craftiest hackers try to cover their tracks and avoid detection. Often, they hope to continue using your system to distribute software illegally, probe other networks, or launch attacks against other systems. They often use 'rootkits' to help them remain undetected. Sony's Trojan horse employed rootkit-like capabilities to hide itself from the user.

Rootkits are programs and patches that hide important information such as process, disk, network activity. They come in many flavors and vary in sophistication from simple application replacements (such as hacked versions of ls) to kernel modules that are nearly impossible to detect.

Host-based intrusion detection software such as OSSEC is used to monitor systems for the presence of rootkits. There are also rootkit finder scripts (such as chrootkit, chrootkit.org) that scan the system for known rootkits.

Although programs are available to help administrators remove rootkits from a compromised system, the time it takes to perform a thorough cleaning would probably be better saving data, reformatting the disk, and starting from scratch. The most advanced rootkits are aware of common programs and try to thwart them.

# Packet filtering

If you're connecting a system to a network that has Internet access, you must install a packet-filtering router or firewall between the system and the outside world. As an alternative, some systems let you implement packet filtering software on the system itself, an option we discuss starting on page 935. Whatever