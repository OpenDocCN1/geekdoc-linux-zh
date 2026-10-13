7. Let's quickly look through some of the other log files to understand what's going on:

```
# head -5 cron
Mar 17 04:05:00 staging CROND[27157]: (root) CMD
(/usr/bin/mrtg /etc/mrtg/mrtg.cfg)
Mar 17 04:10:00 staging CROND[27160]: (root) CMD
(/usr/bin/mrtg /etc/mrtg/mrtg.cfg)
Mar 17 04:10:00 staging CROND[27161]: (root) CMD
(/usr/lib/sa/sa 1)
Mar 17 04:15:00 staging CROND[27164]: (root) CMD
(/usr/bin/mrtg /etc/mrtg/mrtg.cfg)
Mar 17 04:20:00 staging CROND[27167]: (root) CMD
(/usr/bin/mrtg /etc/mrtg/mrtg.cfg)
```

As expected, the cron log file shows commands and actions taken by the cron daemon. In parenthesis it shows the user account, and also shows the command. If you think someone is using a cron-based program to try and break security, it'll be logged here.

8. If you're ready to become paranoid about people trying to get to your computer, have a look at xferlog or ftp.log, depending on your OS. On my Mac OS X server, for example, the log file shows

```
# cat ftp.log | grep -v taylor
Jan 21 12:24:36 dsl-132 ftp[369]: connection from dsl-155.dsldesigns.com
Jan 21 12:24:40 dsl-132 ftp[369]: FTP LOGIN REFUSED
FROM dsl-155.dsldesigns.com, root
Jan 21 12:28:06 dsl-132 ftp[390]: connection from 63.101.93.250
Jan 21 12:35:40 dsl-132 ftp[412]: connection from dsl-155.dsldesigns.com
Jan 21 19:44:24 dsl-132 ftp[491]: connection from 63.101.93.250
Jan 21 19:45:28 dsl-132 ftp[492]: connection from dsl-155.dsldesigns.com
Jan 21 20:00:39 dsl-132 ftp[516]: connection from 63.101.93.250
Jan 22 09:45:04 dsl-132 ftp[332]: connection from webpac.clemson.edu
Jan 22 12:27:23 dsl-132 ftp[460]: connection from 63.101.93.250
Jan 22 13:34:18 dsl-132 ftp[461]: connection from 63.101.93.250
Jan 24 18:00:40 dsl-132 ftp[369]: connection from dsl-155.dsldesigns.com
Jan 26 22:44:59 dsl-132 ftp[927]: connection from dsl-155.dsldesigns.com
Jan 29 18:27:33 dsl-132 ftp[359]: connection from 157.161.112.208
Jan 29 21:48:12 dsl-132 ftp[378]: connection from
port-212.202-160-251.reverse.qds1.home.de
Jan 29 21:48:13 dsl-132 ftp[378]: ANONYMOUS FTP LOGIN REFUSED
FROM port-212.202-160-251.reverse.qds1.home.de
Feb 6 12:10:23 dsl-132 ftp[525]: connection from 199.98.128.27
Feb 6 15:54:41 dsl-132 ftp[554]: connection from pd955f64e.dip.t-dialin.net
Feb 6 21:52:56 dsl-132 ftp[685]: connection from pd955f64e.dip.t-dialin.net
Feb 6 21:52:58 dsl-132 ftp[685]: ANONYMOUS FTP LOGIN REFUSED
FROM pd955f64e.dip.t-dialin.net
Feb 7 00:01:09 dsl-132 ftp[612]: connection from maptech-inc.com
Feb 7 00:01:12 dsl-132 ftp[613]: connection from maptech-inc.com
Feb 7 00:01:21 dsl-132 ftp[614]: connection from maptech-inc.com
```