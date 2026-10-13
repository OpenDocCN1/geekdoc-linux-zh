
5. Many users like to keep track of the entire number of bytes sent from their server to calculate the approximate percentage of bandwidth utilized per day. This is field ten, and the analysis is easier than the earlier examples:

```
# awk '{ sum += $10} END { print "total = " sum/1024 " Kb" }' access_log
```

total = 41583.9 Kb

This equates to a reasonable transfer rate of 2.25MB/hour (41583÷18)÷1024.

6. The other log files are also worth a quick peek. The agent_log is just the Web browser identification string from each visitor:

```
# head agent_log
```

```
Woko robot 3.0
Mozilla/4.0 (compatible; MSIE 5.5; Windows 98)
Mozilla/4.0 (compatible; MSIE 5.5; Windows 98)
Mozilla/4.0 (compatible; MSIE 5.5; Windows 98)
Mozilla/4.0 (compatible; MSIE 5.5; Windows 98)
Mozilla/4.0 (compatible; MSIE 5.5; Windows 98)
Mozilla/4.0 (compatible; MSIE 5.5; Windows 98)
Woko robot 3.0
Mozilla/4.0 (compatible; MSIE 5.0; AOL 7.0; Windows 98; DigExt)
Mozilla/4.0 (compatible; MSIE 5.0; AOL 7.0; Windows 98; DigExt)
```

![](img/5ced0c78d748bd190e9027e5549a3622_330_0.png)

> Fair warning: Some Apache Web server configurations don't record this information, and others only include it in the access_log.

Again, the powerful combination of sort|uniq -c|sort -rn|head will reveal the most commonly used browsers:

```
# sort agent_log | uniq -c | sort -rn | head
```

```
1049 Mozilla/4.0 (compatible; MSIE 5.0; Windows 98; DigExt)
816 Mozilla/4.0 (compatible; MSIE 6.0; Windows 98)
732 Mozilla/4.0 (compatible; MSIE 5.01; Windows NT 5.0)
619 Mozilla/4.0 (compatible; MSIE 5.5; Windows 98; Win 9x 4.90)
604 Mozilla/4.0 (compatible; MSIE 5.5; Windows 98)
458 Mozilla/4.0 (compatible; MSIE 5.5; Windows NT 5.0)
434 Mozilla/4.0 (compatible; MSIE 5.01; Windows 98)
353 Mozilla/4.0 (compatible; MSIE 5.5; Windows NT 4.0)
326 Mozilla/5.0 (Windows; U; WinNT4.0; en-US; rv:0.9.4) Gecko/3 Netscape/6.2
287 Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0)
```

Given that any agent with MSIE in its string is Microsoft Internet Explorer, this shows quite graphically that Internet Explorer certainly does lead the Web browser pack by quite a margin (of the 5,678 browser agents listed in this top ten list, all but 326 (5.7%) are MSIE).

7. The referer_log is somewhat interesting, but it takes a bit of data massaging to see what's really inside. The file contains a list of the last URL someone was at before visiting a Web site on this server:

```
# head -5 referer_log
http://search.yahoo.com/search/msie?o=1&i=ia&fd&p=trivia+games&b=121&h=s -> /
http://www.intuitive.com/sites/trivial/index.html -> /sites/trivial/Graphics/intsys.gif
http://www.intuitive.com/sites/trivial/index.html -> /sites/trivial/Graphics/play-the-game.gif
http://www.intuitive.com/sites/trivial/index.html -> /sites/trivial/Graphics/kudos.gif
http://www.intuitive.com/sites/trivial/index.html -> /sites/trivial/Graphics/animated-banner.gif
```

The problem is that many of these URLs prove to be quite long, thus preventing us from doing any meaningful analysis because the URL includes a timestamp, session ID, and so on.

Instead, cut lets us chop out just the base domain name and see what we find:

```
# cut -d / -f3 referer_log | sort | uniq -c | sort -rn | head
9589 www.intuitive.com
164 www.google.com
116 pub43.ezboard.com
115 pub44.ezboard.com
107 forum.fok.nl
48 search.msn.com
47 search.yahoo.com
39 www.dancing.baby.net
34 www.yellow.baby.net
34 images.google.com
```

Some very interesting results!

8. The final log file is error_log, and here again, we're going to see security problems as people try to break into our server:

```
# head -4 error_log
[Mon Mar 18 00:14:54 2002] [error] [client 66.77.73.219] File does not exist: /u/web/intui2/robots.txt
[Mon Mar 18 00:30:47 2002] [error] [client 198.187.235.65] File does not exist: /u/web/intui2/custer
[Mon Mar 18 00:34:45 2002] [error] [client 12.233.27.11] File does not exist: /u/web/intui2/robots.txt
[Mon Mar 18 01:11:07 2002] [error] [client 64.128.250.173] File does not exist: /u/web/intui2/OLD/Images/social-guide-title.gif
```

Again, you can see that the format is very uniform, so you can easily search for does not exist, extract the actual requested file, sort|uniq it, and have a list of the most common incorrect references:

```
# grep "does not exist" error_log | awk '{print $13}' | sort | \
uniq -c | sort -rn | head
```

```
     34 /u/web/intui2/custer
     26 /u/web/intui2/robots.txt
     17 /u/web/intui2/origins/
     15 /u/web/intui2/favicon.ico
     13 /u/web/intui2/origins/Graphics/nav/newswire-off.gif
     13 /u/web/intui2/apps/Graphics/nav/newswire-off.gif
     11 /u/web/intui2/OLD/Images/social-guide-title.gif
     11 /u/web/intui2/OLD/Images/coolweb-ad.gif
      8 /u/web/intui2/coolweb/apps/relayto.cgi
      8 /u/web/intui2/apps/search-everything.cgi
```

More importantly, you can exclude those errors and see what other problems might have arisen:

```
# grep -v "does not exist" error_log | head
[Mon Mar 18 04:48:51 2002] [error] [client 210.106.38.231] Premature end of script headers: /u/web/intui2/cgi-local/etymologic.cgi
[Mon Mar 18 05:24:40 2002] [error] [client 210.183.67.209] Client sent malformed Host header
[Mon Mar 18 07:51:48 2002] [error] [client 206.114.36.6] script not found or unable to stat: /httpd/cgi-bin/PDQ_Cart
[Mon Mar 18 08:16:16 2002] [error] [client 213.77.101.163] script not found or unable to stat: /u/web/intui2/cgi-local/apps/querty.cgi
[Mon Mar 18 08:16:44 2002] [error] [client 213.77.101.163] script not found or unable to stat: /u/web/intui2/cgi-local/apps/querty.cgi
[Mon Mar 18 11:45:20 2002] [error] [client 199.63.5.67] attempt to invoke directory as script: /u/web/intui2/cgi-local/apps
[Mon Mar 18 11:46:31 2002] [error] [client 199.63.5.67] attempt to invoke directory as script: /u/web/intui2/cgi-local/apps
[Mon Mar 18 12:38:40 2002] [error] [client 164.156.231.55] attempt to invoke directory as script: /u/web/intui2/cgi-local/apps
[Mon Mar 18 13:53:23 2002] [error] [client 213.97.216.50] (11)Resource temporarily unavailable: couldn't spawn child process: /u/web/intui2/cgi-local/switcher.pl
[Mon Mar 18 13:53:24 2002] [error] [client 213.98.97.138] (11)Resource temporarily unavailable: couldn't spawn child process: /u/web/intui2/cgi-local/switcher.pl
```

Definitely some things to explore. Why, for example, is there a call to apps/querty.cgi? What's resource temporarily unavailable mean?

We'll re-address Apache issues in the last two hours of the book.

Of all the log files that can be analyzed and explored, few are more interesting than the Web server itself. Armed with basic Unix tools, it proves easy to extract meaningful information and produce rudimentary statistics in just a moment or two.

Analyzing an access_log file is a clear task for a cron-launched script that can produce a report and e-mail it to the Web administrators. This will be left as an exercise to the reader.

## Trimming Log Files with logrotate

Let's put the question of detecting security problems aside for the rest of this hour and look at the issue of managing the log files themselves.

On a busy server, it's not unusual to see log files that are enormous, and adding lines every few seconds. On a busy Web server, for example, a tail -f /var/log/httpd/access_log might well spit out 50–100 lines each minute as the sites are visited.

The challenge is to simultaneously minimize the size of the log files, while still making sure that they're accessible and available as needed.

### Task 16.4: The logrotate Program

Historically, system administrators have written their own scripts to manage and trim log files, but with the latest generation of Linux, there's a very helpful utility included called logrotate, and it does a very sophisticated job of rotating all the log files in /var/log automatically.

1. By convention, the logrotate command is called from cron on a daily basis. Based on the discussion in the last hour, it should be no surprise that it's located in /etc/cron.daily:

```
# cd /etc/cron.daily
# ls
00-logwatch 0anacron makewhatis.cron slocate.cron tmpwatch
00webalizer logrotate rpm sysstat
# more logrotate
#!/bin/sh

/usr/sbin/logrotate /etc/logrotate.conf
```

Before we look at the command, then, let's have a peek at the configuration file.

2. If you think about the task that's being accomplished, you'll start to see the elegance of the logrotate solution. We have a log file that we want to have automatically renamed file.1, and we want file.1 to be renamed file.2, and so on. After a certain count, we want the oldest files to be deleted, so we have a running window of "rotate-frequency" days of events in the past.

The first few lines of the configuration file specify those two key settings:

```
# cat /etc/logrotate.conf
# see "man logrotate" for details
# rotate log files weekly
weekly

# keep 4 weeks worth of backlogs
rotate 4
```
