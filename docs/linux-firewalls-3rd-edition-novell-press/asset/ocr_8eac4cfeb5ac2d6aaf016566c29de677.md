hping2 again provides an easy way to re-create the cause for testing:

```
```
hping2 -k -S -p 25 -P -a 192.168.1.2 192.168.1.2
```
```

The capture through TCPDump is shown next. Notice that the source and destination addresses and ports are the same and that the source port is not incrementing and that it’s also below the ephemeral ports.

```
```
13:42:28.079339 IP 192.168.1.2.25 > 192.168.1.2.25: S 764505725:764505725(0) win 512
13:42:29.079462 IP 192.168.1.2.25 > 192.168.1.2.25: S 2081780101:2081780101(0) \
win 512
13:42:30.079461 IP 192.168.1.2.25 > 192.168.1.2.25: S 390202112:390202112(0) win 512
```
```

# ## Recording Traffic with TCPDump

While consulting for a small Internet provider, I noticed that there was a routine and significant spike in network traffic at about 3 a.m. every morning and lasting anywhere from 15 minutes to an hour. My goal was to determine the cause of this traffic spike. Because the traffic was routine and at an odd hour, my initial thought was that the traffic was the result of an automatic update process for the servers on the network.

Most of the servers in the network were running Debian Linux and using apt-proxy. This meant that only one local server would contact the off-site Debian update servers and obtain any updates necessary. All the other servers in the local network would then contact that local master server. This setup cut the Internet utilization immensely.

Although the master server could certainly be a contributing factor, I didn’t feel that there would be enough update traffic on a nightly basis to warrant such a significant spike in traffic. My assumption was confirmed when I looked at the update schedule on the master server and found that it was actually looking for updates at a different time period, and thus it wasn’t contributing to the 3 a.m. spike at all.

With that cause eliminated, I needed to look at the traffic itself at 3 a.m. However, I wasn’t really looking forward to staying awake until that hour, and if I was awake, I might not be in shape to read a packet trace. Enter cron. By using cron to fire TCPDump, I could capture the packet trace to a file for later analysis. No great surprise here and I wasn’t breaking any new ground, but it seemed like a fair solution to the problem. I configured the switch to copy packets to the port on which the monitoring machine was connected and got to work on the TCPDump portion.

TCPDump offers a couple features that come in handy for this type of trace. The first feature is the capability to write the output to a file (record, as you will) and then read that file in later (playback). The second helpful feature is the capability to exit after capturing a certain number of packets. Granted, I could’ve used another means to stop the packet trace, such as