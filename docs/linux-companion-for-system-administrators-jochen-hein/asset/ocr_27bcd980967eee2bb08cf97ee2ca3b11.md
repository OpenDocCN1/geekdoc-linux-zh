# 122 CONFIGURATION AND ADMINISTRATION

| Additional Information and Sources |
|---||
| ftp server: | ftp.informatik.rwth-aachen.de |
| ftp path: | pub/Linux/local/packs/APSfilter |
| File name: | aps-48.tgz |
| Size: | about 130 Kbytes |

# 4.6.3 Printing on other network printers

In many networks, not all printers can be accessed via TCP/IP; often they can only be accessed via the NetWare protocol or the protocol of the Windows network. Since LINUX can be integrated into both networks, it is possible to use these printers as well.

If the IPX system is installed and configured (see Section 20.1), it is possible to print to NetWare printers by means of the command `nprint`. If you include a `nprint` call in an input filter of the `lpr` system, you can use a LINUX computer as a gateway between the different systems.

Printers on a Windows network can be accessed by means of `smbclient`. This program is part of the `samba` package; more information on this package can be found in Section 20.2.

# 4.7 System logs

Every UNIX system keeps a series of log files for the purpose of system behaviour monitoring and error detection. A generally accessible interface by means of which programs can write log files is the `syslogd`. This daemon is configured by entries in the file `/etc/syslog.conf`. Depending on their origin or importance, it allows messages to be displayed or redirected into different files. In networked environments it is possible to have the log files kept by a special computer, known as the log host.