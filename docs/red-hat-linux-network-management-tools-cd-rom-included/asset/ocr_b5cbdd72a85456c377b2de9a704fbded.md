include an entry for trap processing. Listing 8.3 shows the standard Linux `syslog.conf` with the appropriate trap entry added (see line 25).

# **Listing 8.3 Standard `syslog.conf` file with trap entry**

```
```
1   # Log all kernel messages to the console.
2   # Logging much else clutters up the screen.
3   *kern.*
4       /dev/console
5
6   # Log anything (except mail) of level info or higher.
7   # Don't log private authentication messages!
8   *.info;mail.none;news.none;authpriv.none
9       /var/log/messages
10
11  # The authpriv file has restricted access.
12  authpriv.*
13      /var/log/secure
14
15  # Log all the mail messages in one place.
16  mail.*
17      /var/log/maillog
18
19  # Everybody gets emergency messages, plus log them on
20  # another machine.
21  *.emerg
22      /usr/bin/omail
23
24  # Save mail and news errors of level err or higher in a
25  # special file.
26  uucp,news.crit
27      /var/log/spooler
28
29  # Save boot messages also to boot.log
30  local7.*
31      /var/log/boot.log
32
33  local0.*
34      /var/log/trapd.log
35
36  #
37  # INN
38  #
39  news.crit
40      /var/log/news/news.crit
41  news.err
42      /var/log/news/news.err
43  news.notice
44      /var/log/news/news.notice
```
```

The new line defines the `syslog` entry that the **snmtrapd** uses when posting messages to the `syslogd` process. The entry indicates that all messages from the `local0` category will be collected. Note that all messages obtained will be saved to the `/var/log/trapd.log` file.