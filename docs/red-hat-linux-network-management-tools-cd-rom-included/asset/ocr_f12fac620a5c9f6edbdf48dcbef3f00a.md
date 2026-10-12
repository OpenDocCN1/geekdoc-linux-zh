it creates a series of files in the directory specified by the `WorkDir` command. Assume, for example, that the `cisco.conf` file contains the following sample entries:

```
WorkDir: /usr/mrtg/www
Target[10.0.2.75.1]: 1:public@10.0.2.75
```

The following files will be created in the `/usr/mrtg/www` directory:

```
10.0.2.75.1-day.gif
10.0.2.75.1-month.gif
10.0.2.75.1-week.gif
10.0.2.75.1-year.gif
10.0.2.75.1.html
10.0.2.75.1.log
10.0.2.75.1.old
```

All of these files have the prefix of the IP address and the interface number and represent the device and port being monitored by MRTG. The `10.0.2.71.1-html` file contains the high-level report, in HTML, previously shown in Figure 9.1. When viewing the MRTG reports, use this file and a standard Web browser to display the interface performance graphs. The files with the `.gif` extension are the four graphs that show the daily, monthly, weekly, and yearly usage in bytes per second of the device that the `10.0.2.75.1.html` report file uses. The `10.0.2.75.1.log` and `10.0.2.75.1.old` files contain the SNMP polled data used to build the graphs.

For every interface monitored by MRTG, these seven files will be created automatically. Another good thing about MRTG is that the reports and data files don't consume a large amount of disk space. In fact, MRTG uses a unique method of data storage to minimize the amount of space used in the historical graphs.

To ensure that MRTG captures consistent and complete information from the monitored devices, the MRTG program must be run at regular intervals. One of the best ways to achieve this is to use the *cron* facility. Since the daily graph, which is available on the MRTG report, is averaged over a five-minute period, it is reasonable that *mrtg* should be run every five minutes. A sample `crontab` entry that would do just this is shown here:

```
0,5,10,15,20,25,30,35,40,45,50,55 * * * * /usr/bin/mrtg \
/usr/mrtg/www/mrtg.conf
```