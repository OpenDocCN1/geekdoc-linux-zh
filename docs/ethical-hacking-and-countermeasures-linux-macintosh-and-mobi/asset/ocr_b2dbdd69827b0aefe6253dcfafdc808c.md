be used to verify the integrity of the files. This first AIDE database is a snapshot of the system in its normal state and the yardstick by which all subsequent updates and changes are measured. AIDE can be configured to customize how detailed the checks should be. It recursively traverses each directory on the host system to determine what files should be included in the database. Files are matched against the files and path names that the user specifies. Before using AIDE, an initial database should be created. The command that creates a database for AIDE is aide -i -c /etc/aide.conf.

This command creates the first picture of the file system. The database should be created before hooking the system into the network. AIDE can be run without the -i option, to check for any changes made. If the changes seem to be authentic, then the user can update the database with the -u option to prevent AIDE from reporting changes since the last update. The -u option will not overwrite the database. The following are a few status check definitions in AIDE to be looked for:

+   * *i (inode number):* A change in inode number indicates that the file has been removed or the file name has been changed.

+   * *s (file size):* A change in file size indicates that the content of the file has been changed.

+   * *m (modification time):* This shows the time when the file was last modified.

# Linux Tools: Encryption

# Stunnel

Stunnel is a program that allows the user to encrypt arbitrary TCP connections inside SSL (Secure Sockets Layer) and is available on both UNIX and Windows. Stunnel lets the user secure non-SSL-aware daemons and protocols (like POP3, IMAP, NNTP, and LDAP) by having Stunnel provide the encryption, without changing the daemon's code. Stunnel provides the same functionality of inetd with the addition of SSL encryption. Stunnel also supports TCP Wrappers.

# OpenSSH/SSH

SSH (Secure Shell) is a program for logging into a remote machine and for executing commands on a remote machine. It provides secure encrypted communications between two hosts over an insecure network. It is described as an R command replacement with encryption and RSA authentication.

# GnuPG

GnuPG is a replacement for PGP. Because it does not use the patented IDEA algorithm, it can be used without restrictions.

# Linux Tools: Log and Traffic Monitors

# MRTG (Multi-Router Traffic Grapher)

The Multi-Router Traffic Grapher (MRTG) is a tool to monitor the traffic load on network links. MRTG generates HTML pages containing PNG images, which provide a live visual representation of the traffic. MRTG consists of a Perl script that uses SNMP to read the traffic counters of routers and a fast C program that logs the traffic data and creates graphs representing the traffic on the monitored network connection.

The following are the key features of MRTG:

+   * It is portable.

+   * It comes with a set of configuration tools that make configuration and setup very simple.

+   * The look of the Web pages produced by it is highly configurable.

# Swatch

Swatch was originally written to actively monitor messages as they are written to a log file via the UNIX syslog utility. For a simple demonstration, a user can type `perl swatch --examine=FILENAME`, with FILENAME being the file that the user would like to see the contents of.

# Timbersee

Timbersee is a program very similar to Swatch. It is used to monitor log files for important messages using regular expressions, but differs in that it can watch more than one log file at a time and does not fork off extra processes.