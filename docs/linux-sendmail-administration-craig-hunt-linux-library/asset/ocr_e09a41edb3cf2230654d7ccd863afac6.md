script invoked. The sendmail script is invoked indirectly from the runlevel directories\sby the S80sendmail script (see Listing 3.2). An examination of that script shows that it
is just a symbolic link to the real sendmail script.

# Listing 3.2 The Sendmail Link for Runlevel 3

```
```bash
[crag]$ cd /etc/rc.d/rc.3
[crag]$ ls -1 S80sendmail
1rw-xr-x 1 root root 02 26 1999 S80sendmail -> ../init.d/sendmail
```
```

To enable or disable the sendmail start-up for a specific runlevel, simply add or
remove the symbolic link in that runlevel's directory. And of itself this would be simple
enough, but Linux systems make it even easier by providing tools to manage the runlevel
directories.

# Enabling Sendmail with tksysv

tksysv is an X Windows tool for the purpose of controlling scripts started at
each runlevel. Figure 3.1 shows the main tksysv screen.

# Figure 3.1 Enabling Sendmail with tksysv

| SYSV Runlevel Manager, v0.92 |
| Available: | 2 | 3 | 4 | 5 |
|---|---|---|---||}{
| routed | | keytable | nfs | autofs |
| rstats | network | sendmail | autofs | keytable |
| rusersd | random | keytable | sendmail | gpm |
| rwhod | t sound | httpd | httpd |
| sendmail | a crowd | sound | sound | xfs |
| single | r pcmia | vmware | xfs | smb |
| smb | l | | | linuxconf |
| syslog | keytable | linuxconf | linuxconf |
| vm | gno | local | |
| xfs | | | | |
| yphbind | autofs | rstats | rstats | rstats |
| ypasswdd | sound | rusersd | rusersd | rusersd |
| ypserv | httpd | rwhod | rwhod | rwhod |
| Add | nfs | ypasswdd | ypasswdd | ypasswdd |
| Remove | t rstatsd | dhcpd | dhcpd | dhcpd |
| Edit | e rusersd | named | named | named.rmpc |
| Execute | rwhod | routed | routed | routed |
| | sendmail | ypserv | ypserv | |
| | ypasswdd | yphbind | |