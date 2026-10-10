another cron job to kill the TCPDump capture, but I thought that using TCPDump’s native capability was the quickest and easiest solution.

All the TCPDump commands I’ve shown so far in this chapter have used expressions such as **port 80** or **host <ns>.<ns>.<ns>.<ns>**. Expressions are helpful when you’re looking for specific and known traffic. However, expressions aren’t of much help when you’re unsure of what exactly you’re searching for, as was the case here. The best option was to capture everything and then work on it later during playback.

The two TCPDump options of interest that haven’t been covered yet in the chapter are **-w** and **-c**. The **-w** option causes TCPDump to place the raw output into the specified file so that it can later be fed back through TCPDump. The resulting file is in TCPDump’s native format and is thus not readable by a plain-text pager such as **cat**, **less**, or **more**. The **-c** option informs TCPDump that it should exit after it captures <n> packets. Getting <n> correct seemed to be the most difficult part of this capture.

The capture results needed to show me only basic information about the packet, including source and destination, as well as a few bits of the packet. To that end, the TCPDump command was rather easy to craft:

```
/usr/sbin/tcpdump -c 25000 -w dumpfile -n
```

In this command I have TCPDump exiting after capturing 25,000 packets, writing the capture to a file called **dumpfile**, and not performing DNS queries for the source and destination. Getting to this command did require some level of testing to see just how long it took to capture 25,000 packets and what information was included in the capture. After it was tested, I entered the command into cron with this schedule:

```
5 3 * * * /usr/sbin/tcpdump -c 25000 -w dumpfile -n
```

That is, every morning at 3:05 a.m. the capture would take place. Then at a saner hour, like 11 a.m. when I got out of bed, I’d look to see whether indeed there was traffic the prior evening that required me to look at the **dumpfile**. If there was traffic, I’d log in to the server and run a command to read the **dumpfile**:

```
tcpdump -r dumpfile -X -vv
```

Running this command gave me an idea of what traffic was out there. Intermingled with the normal traffic was an FTP conversation between one of the ISP’s larger customers and another host on the Internet. The FTP traffic was easily the most frequent packet I was seeing within the trace. Another nights’ packet trace confirmed it. I had the ISP contact its customer to find out whether this was known activity and, if so, to let the customer know that it might be going over its bandwidth allocation for the month.