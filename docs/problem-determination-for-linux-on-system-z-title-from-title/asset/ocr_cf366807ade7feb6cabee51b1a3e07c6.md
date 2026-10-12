```
04/01/2008 03:09:23 IWL0080I Max. number of clients = 300
04/01/2008 03:09:23 IWL0032I Number of worker threads = 32
04/01/2008 03:09:23 IWL0040I Script file name = PingJDBCRead_Gold.jxs
04/01/2008 03:09:23 IWL0020I Percent element delay = 150%s
04/01/2008 03:09:23 IWL0062I Startup delay = 1500 ms
04/01/2008 03:09:23 IWL0064I Max. connect timeout = 30 s
04/01/2008 03:09:23 IWL0065I Max. read/write timeout = 60 s
04/01/2008 03:09:23 IWL0081I Max. errors before exiting = 500
04/01/2008 03:09:23 IWL0077I Console print = on
04/01/2008 03:09:23 IWL0063I Validate length checking = on
04/01/2008 03:09:23 IWL0067I Dynamic DNS = off
04/01/2008 03:09:23 IWL0022I Dynamic cookies = on
04/01/2008 03:09:23 IWL0057I XML stats interval = 0 s
04/01/2008 03:09:23 IWL0041I Script repeat = 0
04/01/2008 03:10:25 IWL0046W HTTP read timeout encountered, server=9.12.4.243,
uri=/trade/servlet/PingJDBCRead, clientId=1.
04/01/2008 03:17:07 IWL0046W HTTP read timeout encountered, server=9.12.4.243,
uri=/trade/servlet/PingJDBCRead, clientId=18.
```

To diagnose this problem, we first tried a quick check with the **top** command on each server to see what was going on. The HTTP and DB2 servers appeared to have no problem in handling the workload. This can be seen by the way that the resources are being utilized in both servers, as shown in Example 11-2.

# Example 11-2 HTTP server utilization

```
top - 18:01:05 up 3 days, 20:59, 1 user, load average: 0.00, 0.00, 0.00
Tasks: 50 total, 2 running, 48 sleeping, 0 stopped, 0 zombie
Cpu(s): 1.0%us, 0.3%sy, 0.0%ni, 98.7%id, 0.0%wa, 0.0%hi, 0.0%si, 0.0%st
Mem: 505168k total, 427472k used, 77696k free, 115524k buffers
Swap: 719896k total, 0k used, 719896k free, 129576k cached

PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
2598 nobody 20 0 231m 7016 1932 S 0.7 1.4 0:06.30 httpd
28770 nobody 19 0 232m 8152 1900 S 0.7 1.6 0:03.54 httpd
2600 nobody 21 0 230m 6836 1936 S 0.3 1.4 0:06.37 httpd
1 root 16 0 848 316 264 S 0.0 0.1 0:04.13 init
2 root RT 0 0 0 0 S 0.0 0.0 0:00.00 migration/0
3 root 34 19 0 0 0 S 0.0 0.0 0:00.04 ksoftirqd/0
```