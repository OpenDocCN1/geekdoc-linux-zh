# LIDS (Linux Intrusion Detection System)

LIDS has a built-in port scan detector that runs in the kernel and logs any offending host via syslog.

# Password Cracking in Linux

# Tool: John the Ripper

John the Ripper is designed to find standard UNIX eight-character DES-encrypted passwords by standard guessing techniques. This tool cracks standard and double-length DES, MDS, and Blowfish algorithms. Because this tool is available on different platforms, it can be transferred from one machine to another. The user can specify the word list or the rules that are to be used. Any session can be suspended or restarted, and the status of an interrupted or running session can be obtained.

The users or the groups that are to be targeted can also be specified. It can run by passing a password file on the command line (which is usually a copy of /etc/shadow). Because it contains encrypted passwords, it should be made readable only by root.

Figure 1-8 shows a screenshot from John the Ripper.

# Tool: Slurpie

This tool can run in distributed environments. It provides a password file fed to the program to run on a single host or multiple hosts. Because it will run on multiple hosts at the same time, it can speed up the cracking process considerably.

# Firewall in Linux: IPTables

Linux handles packet filtering at the kernel level. Data entering or passing through the system will only pass if it matches a set of rules, called filters, that allow the packet. Filters can sort packets by their protocol, source and destination address, or target port.

Different kernels use different filtering programs. The 2.2 kernels used IPChains. Since kernel 2.4, the filtering program has been IPTables. IPTables has many more features than IPChains.

![](bbox=[0.18, 0.58, 0.79, 0.88])

Figure 1-8 This is the John the Ripper password-guessing screen.