# **Running Standalone Servers** 613

| Service Name | Description |
| :--- | :--- |
| rpcsvcgssd | Server that manages security for NFS version 4 servers and provides security for RPC-based protocols such as NFS. |
| rsync | Server that supports remote copying of files. You have to enable xinetd for this service to run. |
| saslauthd | Supports authentication using the Cyrus-SASL (Simple Authentication and Security Layer) software. |
| sendmail | Moves mail messages from one machine to another. Start this service if you want to send mail from your Fedora Core system. If you don’t plan to use your Fedora Core system as a mail server, don’t start the sendmail server because it can slow down the booting process and consume unnecessary resources. |
| services | Lists active services that are being managed by xinetd. This server requires xinetd to run. |
| sgi_fam | Implements a file alteration monitor (FAM) that can be used to get reports when files change. |
| smartd | Monitors the Self-Monitoring, Analysis and Reporting Technology (SMART) system built into many ATA, IDE, and SCSI-3 hard drives. This daemon can monitor the reliability of the hard drive and predict drive failures, and can perform various self-tests of the drives. |
| smb | Starts and stops the Samba smbd and nmbd services that support LAN Manager services on a Fedora Core system. |
| snmpd | Simple Network Management Protocol (SNMP) service used for network-management functions. |
| snmptrapd | Receives and logs SNMP messages known as TRAP and INFORM messages. |
| squid | A caching server for Internet objects — anything that can be accessed through HTTP and FTP. |
| sshd | Server for the OpenSSH (Secure Shell) secure remote login facility. |
| syslog | Service used by many other programs (including other services) to log various error and status messages in a log file (usually, the /var/log/messages file). Always run this service. |
| telnet | Server that supports TELNET remote login sessions. You have to enable xinetd for this service to run. |
| tux | The kernel-based HTTP server. |
| udev | Manages device nodes dynamically. You can use it to manage the device files in the /dev directory by editing udev’s configuration file /etc/udev/udev.conf. |

(continued)

*(continued)*

**Book VIII**  
**Chapter 1**  
**Managing the Servers**