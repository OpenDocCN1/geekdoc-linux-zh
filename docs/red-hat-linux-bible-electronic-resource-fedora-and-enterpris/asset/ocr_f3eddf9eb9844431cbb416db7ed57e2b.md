# mozilla /var/www/html/usage/index.html

The output report shows a 12-month summary of Web server activity. On the bar chart, for each month a green bar represents the number of hits on the Web site, the dark blue bar shows the number of different files hit, and the light blue bar shows the number of pages opened. It also shows data for the number of visits and the number of sites that visited in the right column. The amount of data transferred, in kilobytes, is displayed as well.

Figure 21-5 shows an example of a webalizer output file for a Web server that has been running for several months.

![](bbox=[0.05, 0.25, 0.6, 0.65])

**Figure 21-5:** Webalizer displays Web data in chart and column formats.

Below the chart, a table shows daily and monthly summaries for activity during each month. Users can click the name of a month to see detailed activity.

> **TIP:** Because webalizer supports both common log format (CLF) and combined log format, it can be used to display information for log files other than those produced for Apache. For example, you could display statistics for your FTP server or Squid server.

Several other software tools are available for analyzing transfer statistics. The accompanying sidebar on statistics packages available for Red Hat Linux describes some of these tools.