+   6. The ports from 0 to 1023 are reserved for system use.
+   7. The -a option lists all listening or connected ports, while -t specifies TCP ports only and -p reports on the listening or active process names, so netstat -atp would produce this result.
+   8. When determining which services to enable on a server, ask: Do I need the service? Is it secure by default? Does the service need updates? Bonus points if you think to ask: Do I feel lucky?
+   9. Use the service xinetd stop command to shut down the service altogether.
+   10. The syslog port is port 514, which is used to transmit and receive syslog reports from remote systems (if syslogd was started with the -r option).
+   11. The Tripwire program creates a checksum for each protected file and sends a notification whenever any of those files are changed.
+   12. The Nessus server process is nessusd.
+   13. Security through obscurity is a type of wishful thinking by which people convince themselves that if nobody is told how something works, they'll have a more difficult time breaking or breaking into that something. I don't know how well it works, but it's a weak idea conceptually, since there are many ways to attack even the least illuminated of black boxes.
+   14. Social engineering is a type of salesmanship by which a croaker attempts to gather useful information about an intended target system or user. It's the computer version of the person who stole your wallet calling you up, claiming he's from the bank, and asking for your ATM PIN. Many people have been suckered into giving up PINs or passwords by confident, unethical predators.
+   15. Your answers may vary, but I'll provide a few. Lock the door and restrict access to the key. Leave flopp y disk drives, USB ports, and other means of getting access to the system unconnected, or disabled via a password-protected BIOS. Use locking racks. Don't store expensive equipment or data in your cubicle.

# Module 10: The Domain Name Service (DNS)

+   1. A primary name server for a domain is simply a DNS server that knows about all hosts and subdomains existing under its domain.
+   2. The root servers.
+   3. Subdomains are used to further divide domains into smaller sections for ease of administration.
+   4. The three types are
+      Primary servers are authoritative for a particular domain; all domain configuration files reside here.
+      Secondary servers work as backups and as load distributors.
+      Caching servers contain no configuration files for any particular domain but keep a local copy of the result from a query.
+   5. The server statement tells BIND specific information about other name servers it might be dealing with.