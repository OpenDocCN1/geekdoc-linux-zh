formatting in your logs. Here are some of those tools and where you can find them:

+   ■ WebTrends: http://www.webtrends.com/  
+   ■ Wusage: http://www.boutell.com/wusage/  
+   ■ wwwstat: http://www.ics.uci.edu/pub/websoft/wwwstat/  
+   ■ http-analyze: http://www.netstore.de/Suply/http-analyze/  
+   ■ pwebstats: http://www.unimelb.edu.au/pwebstats.html  
+   ■ WebStat Explorer: http://www.webstat.com/  
+   ■ AccessWatch: http://netpresence.com/accesswatch/

The best way to find out which one works for you is to try them out, or at least visit their Web sites for feature comparisons. Two utilities that I find very useful are Wusage and wwwstat. Wusage is my favorite commer- cial log-analysis application. It is highly configurable and produces great graphical reports using the company’s well-known GD graphics library. I also like the free wwwstat program. It is written in Perl, so you need to have Perl installed on the system on which you want to run it.

# Maintaining server log files

On Apache sites with high hit rates or many virtual domains, the log files can become huge in a very short time, which could easily cause a disk crisis. When log files become very large, rotate them. You have two options for rotating your logs: use a utility that comes with Apache called rotatelog, or use logrotate.

# Using rotatelog Apache comes with a support tool called rotatelog. You can use this program as follows:

```
TransferLog " | /path/to/rotatelog log file rotation time in seconds"
```

For example, if you want to rotate the access log every 86,400 seconds (24 hours), use the following line:

```
TransferLog " | /path/to/rotatelog /var/logs/httpd 86400"
```

You will have each day’s access log information stored in a file called /var/logs/httpd.nnn, where nnn represents a long number.