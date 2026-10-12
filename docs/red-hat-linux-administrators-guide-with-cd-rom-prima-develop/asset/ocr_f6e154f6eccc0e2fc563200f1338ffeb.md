The -bd option starts up sendmail as a daemon, which then runs in the background. The daemon awaits connections to port 25, at which time it will request information about the e-mail message itself and then either pass it along or drop it. You can use other options when starting up sendmail. Rather than running sendmail as a background daemon, you can use the commands describes in Table 17.1.

Table 17.1 Options That You May Use to Define How sendmail Will Run
| Mode | Alias | Description |
| :--- | :--- | :--- |
| ba | | Use ARPANet protocols |
| bD | | Run as a daemon, but do not fork |
| bd | smtpd | Run as a daemon |
| bH | purgestat | Purge persistent host status |
| bh | hoststat | Print persistent host status |
| bi | newaliases | Rebuild alias database |
| bm | | Be a mail sender |
| bp | mailq | Print contents of the mail queue |
| bs | | Run SMTP on standard input |
| bt | | Enter test mode and resolve addresses |
| bv | | Verify, but don't collect or deliver |


Many of these options are used to check the status of the running sendmail process or for debugging purposes. Also, instead of executing the absolute path to sendmail along with the options, you can simply use the alias name for the same command. The most popular of these is mailq, which prints the contents of the e-mail queued up and waiting to be delivered.

To test the running version of sendmail, use telnet to access port 25 on the localhost machine. This command verifies that the version is correct. In a terminal window of same machine on which you installed sendmail, enter the following:

```
telnet localhost 25
```