# The Results

First off, let’s check on the .netstatlog file, shown in Listing 10-13.

```
$ tail -f /Users/taylor/.netstatlog

time=1063981801;snt=14386;re=24;rec=15700;dup=444;00=555;creq=563;cacc=17;reto=158

time=1063982400;snt=17236;re=24;rec=20088;dup=454;00=848;creq=570;cacc=17;reto=158

time=1063983000;snt=20364;re=24;rec=25022;dup=589;00=1181;creq=582;cacc=17;reto=158
```

Listing 10-13. The last three lines of the .netstatlog file that results from a crontab entry running the getstats script on a regular interval

It looks good. Listing 10-14 shows the results of running netperf and what it has to report.

```
$ netperf

Netstat is currently reporting the following:
52170128 packets sent, with 16927 retransmits (0%) and 2722 retransmit timeouts (0%)
20290926 packets received, with 129910 dupes (0.600%) and 18064 out of order (0%)
39841 total connection requests, of which 123 were accepted

Analyzing trends...

(Analyzed 6 netstat log entries for calculations)
```

Listing 10-14. Running the netperf script to analyze the .netstatlog file

# Hacking the Script

You’re likely already noticed that rather than using a human-readable date format, the getstats script saves entries in the .netstatlog file using epoch time, which represents the number of seconds that have elapsed since January 1, 1970. For example, 1,063,983,000 seconds represents a day in late September 2003. The use of epoch time will make it easier to enhance this script by enabling it to calculate the time elapsed between readings.

# #78 Renicing Tasks by Process Name

There are many times when it’s useful to change the priority of a task, whether a chat server is supposed to use only “spare” cycles, an MP3 player app is not that important, a file download has become less important, or a real-time CPU monitor needs an increase in priority. You can change a process’s priority with the renice command; however, it requires you to specify the process ID, which can be a hassle. A much more useful approach is to have a script like the one in Listing 10-15 that matches process name to process ID and automatically renices the specified application.