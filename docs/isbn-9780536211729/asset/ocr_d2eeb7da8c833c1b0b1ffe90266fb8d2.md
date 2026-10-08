# PART
II

# DETECTING AN INTRUSION

This whole book is about reducing the probability, severity, and consequences of intrusions. Be realistic. No system is 100 percent secure and anyone who claims that his system or his products are 100 percent secure is a fool or a liar. 99 percent of the people reading this book will have someone attempt to break into their systems. Without changing your configuration system instead they are encouraged to reread the previous paragraph¹

Perhaps 10–20 percent of people reading this book will suffer a system break-in. Those who are scared by this statistic and are considering another book or switching to another operating system instead are encouraged to reread the previous paragraph!

The suggestions in Part I were a methodical approach to eliminating known security holes in the varying parts of your system and network. Now comes the vigilant watch for intrusion attempts. If following the advice of the previous parts of this book makes your system so secure, why should you care about thwarted attacks? As I write the current versions of all Linux distributions have a known DNS vulnerability, due to a bug in the new version of the named program. By monitoring system and network activity, you may detect these intrusions quickly and eliminate the consequences.

It is important to monitor the security sites discussed in Appendix C so you can update your system when someone gets broken into, before the same exploit happens to pen your systems. However, this is not a cure-all. One of my clients suffered a break-in in late 1999, via FTP, a method that had not been discussed in the security sites (which I had been monitoring very closely while conducting research for this book).

The log files indicated suspicious FTP activity with time-stamps indicating it happened shortly before the cracker installed some files. The logs indicated no email or DNS activity. This was enough to satisfy me as the means of the attack. Certainly, an extremely sophisticated cracker had planted false logs, but this is very unusual and this incident

> ¹ My server does not provide RPC services, telnet, ftp, or cracker Trojans by monitoring these ports, I know when attacks are directed to these ports and my systems lock these crackers out automatically. This might be considered as acting as a honeypot; that is, providing something sweet to attract crackers away from something more valuable or sensitive.