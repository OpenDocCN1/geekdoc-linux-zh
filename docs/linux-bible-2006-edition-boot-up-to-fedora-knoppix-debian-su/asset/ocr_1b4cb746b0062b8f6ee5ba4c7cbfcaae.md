# 206 Part II ♦ Running the Show

| Table 6-2 (continued)
| System Logs Name | Filename | Description |
| --- | --- | --- |
| Update Agent Log | up2date | Contains messages resulting from actions by the Red Hot Update Agent. |
| X.Org X11 Log | Xorg.0.log | Includes messages output by the X.Org X server. |
| a | gdm/:0.log | Holds messages related to the login screen (GNOME display manager). |
| a | samba/log.smbd | Shows messages from the Samba SMB file daemon. |
| a | squid/access.log | Shows messages relating to the proxy/caching server. |
| a | vsfptpd.log | Contains messages relating to transfers made using the vsFTPpd daemon (FTP server). |
| a | sendmail | Shows errors recorded by the sendmail daemon. |
| a | uucp | Shows status messages from the UNIX to UNIX Copy Protocol daemon. |

+   * Indicates a log file that is not contained in the System Logs window. Access these files directly from /var/log.

# The Role of Syslogd

Most of the files in the /var/log directory are maintained by the syslogd daemon. The syslogd daemon is the System Logging Daemon. It accepts log messages from a variety of programs and writes them to the appropriate log files. It is better than having every program write directly to its own log file because it enables you to centrally manage how log files are handled. It is possible to configure syslog to record varying levels of detail in the log files. It can be to ignore all the critical messages, or it can record every detail.

The syslogd daemon can accept messages from other computers on your network. This is particularly handy because it enables you to centralize the management and reviewing of logs from many systems on your network. If a system is broken, the cracker cannot delete or modify log files because those are stored on a separate computer. It is important to remember, however, that log messages are not, by default, encrypted. Anyone tapping into your local network can eavesdrop on those messages as they pass from one machine to another. Also,