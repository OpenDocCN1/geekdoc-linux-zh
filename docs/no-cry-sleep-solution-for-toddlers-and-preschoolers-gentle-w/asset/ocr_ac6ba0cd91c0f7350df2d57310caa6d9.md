by xinetd is in.ftpd. This is a link to the wu-ftpd command. xinetd will run a file called wu-ftpd located in the /etc/xinetd.d directory.

You can use numerous configuration options to tailor your FTP server to your site’s particular needs. WU-FTPD makes use of several configuration files located in the system’s /etc directory. All begin with the pattern ftp. The primary configuration file is named ftpacess. Here, you provide basic server information and access for specified directories.

The ftphosts, ftpusers, and ftpgroups files control access by systems, particular users, and groups. ftpconversions specifies how archive and compression operations are to be performed on files before or after they are transferred. xferlog is the log file that stores a running log of all transactions performed by the server.

# ProFTPD and WU-FTPD Server Tools

Both the WU-FTPD and ProFTPD daemons provide a set of FTP tools you can use to manage your FTP server. With the ftpshut command, you can smoothly shut down a running server, warning users of the shutdown well before it happens. ftpwho can tell you who is currently connected and what they are doing. ftpcount can give you the number of connections currently in effect. Although each daemon has its own set of tools, they perform the same action with much the same set of options. Tools provided by both ProFTPD and WU-FTPD have the same name and options, though ProFTPD provides more information on virtual hosts and has some added options.

# ftpshut

With the ftpshut command, you can have the FTP server shut down at a given time, rather than suddenly shutting it down by killing its process. This gives you the chance to warn users the server is shutting down and not to start any long downloads. ftpshut takes several options for specifying the time and including a warning message. ftpshut takes as its arguments the time until the shutdown, followed by the warning message you want sent to users. The time can be a word such as “now” that effects an immediate shutdown, a + sign with the number of minutes remaining, or a specific time of day indicated by an HHMM format, where HH is the hour in a 24-hour cycle and MM is the minute. The following example shuts down the FTP server in ten minutes, issuing a warning to users:

```
ftpshut +10 "Shutdown in ten minutes"
```

Shutdown disables any new FTP access ten minutes before a scheduled shutdown, though this can be changed using the -l option with the number of minutes you want. Five minutes before a scheduled shutdown, all current connections are disconnected. You can adjust the time with the -d option. The warning message is formatted at 75 characters, and you can use special formatting symbols for in-place substitutions of certain values in the warning message, such as the shutdown time. These symbols are called magic cookies. For example, %s is the shutdown time, %r is the time when new connections are refused, %d is the time when current connections are cut, %m is the maximum number of users, and %l is the local hostname.