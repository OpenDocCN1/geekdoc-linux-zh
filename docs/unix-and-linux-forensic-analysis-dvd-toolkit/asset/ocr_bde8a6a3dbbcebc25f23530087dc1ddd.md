# 206 Appendix A • Implementing Cybercrime Detection Techniques on Windows and *nix

screening routers, application gateways, and so forth). But sensitive files reside, it probably makes sense to audit access to such files, including attempted and successful accesses. In general, it's also a good idea to monitor administrative activities on all devices (and to advertise policy) that IT professionals know they will be held accountable for all official (and unsanctioned) administrative activities they perform.

In some situations—perhaps when an account may be compromised—it may make sense to disable that account (and set up a new account for the old account's user), and then audit subsequent attempts to use the old account. This practice permits administrators to determine whether such activity originates inside or outside the local network boundary and can help to establish an intruder's identity.

The general principle at work here is to audit for suspicious activities, to track administrative activity, and to monitor information or assets of value or interest. By combining these activities into the auditing strategy, it's easier to strike the right balance between audit data volume and the amount of useful information that can be discerned from data.

# Auditing for UNIX and Linux Platforms

Every different distribution and version of UNIX and Linux logs critical audit information in its own way and stores the resultant log files in particular locations using specific platform–default formats. Nevertheless, most UNIX and Linux operating systems support extensive logging capabilities and share numerous common features.

The Syslog daemon (syslogd) is a clearinghouse for all kinds of log information on UNIX and Linux systems. The daemon is a process that directs different system messages to log different files, depending on the type of message and how urgent severe it is. For example, on a FreeBSD system, successful and failed File Transfer Protocol (FTP) logons are shown in the ftp.log file, information about access to Apache Web sites is stored in access_log, and information about failed logons resides in secure.log.

Most networks that incorporate UNIX or Linux systems also set up special network drives to record logging data, so it can all reside in a single centralized location. In addition, the Syslog daemon receives event data from various operating system and user applications (listed in Table A.2); it also stores all log data using a