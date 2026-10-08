# 324 PART 3 | Building a Layered Linux Strategy

> > WARNING

Just because software can be downloaded and installed from the repositories associated with a distribution doesn't mean it is supported or secure. For example, the noted WU-FTPD service is not maintained or secure as this writing. Even though it has not been maintained since 2004, it is still available from the unsupported repositories of some major Linux distributions.

+   • Pure File Transfer protocol (Pure-FTPd)—An actively supported server that can run 100 percent with non-root accounts. For more information, see http://www.pureftpd.org/

+   • Pro File Transfer protocol (ProFTPD)—An actively supported server with a basic configuration similar to the Apache Web server, with respect to the configuration of multiple virtual FTP servers. For more information, see http://www.proftpd.org.

+   • Washington University File Transfer protocol (WU-FTPD)—A commonly used FTP server through the early part of the 2000s. While it is not maintained, it is still available from the Ubuntu University repositories.

# Linux Has Antivirus Systems Too

Antivirus systems, loosely defined, include systems that can detect all types of malware. While not all malware affects an operating system, it can be transmitted by e-mail and be carried by files with common formats. This section covers some of the available malware systems for Linux. On any computer system, malware falls into several categories, which include the following:

+   • Rootkit—A rootkit is malware that can help a black-hat hacker gain administrative control over a computer system.

+   • Spyware—Spyware is malware that collects user information; may include keystroke logging.

+   • Trojan horse—A Trojan horse is a type of malware that hides as a desirable program that facilitates unauthorized access.

+   • Virus—Strictly speaking, a computer virus is a program that can copy itself and infect a computer. Loosely speaking, the term virus refers to all malware.

+   • Worms—Self-replicating malware can send itself to other systems as a worm. A worm is different from a virus in that it does not require direct user involvement to spread.

Responsible Linux administrators include antivirus software on their systems. While there are fewer targeted at Linux, they do exist. One problem associated with Windows operating systems is the number of users who run it with administrative privileges. Linux is configured to discourage running most commands with administrative privileges, it is possible to configure Linux with only the root account. So Linux is not immune. While Linux may be a more difficult target for black-hat hackers, it is still a target. Some Linux applications such as the Apache Web server have a dominant market share.