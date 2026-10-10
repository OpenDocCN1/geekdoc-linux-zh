
obtain time information from other servers on the network using the **Network Time Protocol** (NTP).

![](img/c27875544958897d817484d558c208c8_612_0.png)

You can view and modify the date and time within the BIOS using the BIOS configuration utility on your computer or by using the **hwclock** command.

NTP is one of the oldest Internet protocols still commonly used on the Internet. It is designed to simplify the setting of time and date information on computers across the Internet using UDP port 123. The two NTP daemons that are commonly used on Linux systems are the NTP daemon (**ntpd**) and Chrony NTP daemon (**chronyd**).

# Understanding NTP Strata

NTP uses a hierarchical series of time sources called **strata**. Stratum 0 is at the top of this hierarchy and consists of atomic devices or GPS clocks. Stratum 1 devices obtain their time directly from Stratum 0 devices. Stratum 2 devices obtain their time from Stratum 1 servers, and so on. This organization is shown in Figure 13-4.

The stratum is not an indication of quality or reliability since NTP servers typically obtain time information from multiple time sources (NTP servers) and use an algorithm to determine the most reliable time information. As a result, it is common to find a Stratum 3 device that is more accurate than a Stratum 2 device.

![](img/c27875544958897d817484d558c208c8_612_1.png)

NTP supports up to 256 strata.

![](img/c27875544958897d817484d558c208c8_612_2.png)

**Figure 13-4** A sample strata structure

![](img/c27875544958897d817484d558c208c8_613_0.png)

Most Internet time servers, such as time.apple.com, are Stratum 1 devices.

# Working with ntpd

Most Linux systems use ntpd to provide for NTP functionality. It can act as both an NTP client to obtain time from an Internet time server or an NTP server that other computers can query for time information. Although most Linux distributions install ntpd during the Linux installation process, it can be installed from a software repository if it is not available.

To configure a Linux system as an NTP client using ntpd, you can modify the /etc/ntp.conf file and add lines for different NTP servers the client can query. These servers could be any strata or combinations of different strata.

For example, the following lines in /etc/ntp.conf query three time servers: ntp.research.gov, ntp.redhat.com, and 0.fedora.pool.ntp.org.

```
server ntp.research.gov
server ntp.redhat.com
server 0.fedora.pool.ntp.org
```

![](img/c27875544958897d817484d558c208c8_613_1.png)

Each of the FQDNs listed in the preceding output may point to multiple servers since NTP servers typically have several A (host) records in DNS that list the name FQDN for different IP addresses. This allows NTP requests to be spread across all servers to reduce server load.

If your time differs significantly from the time on these time servers, you must first stop ntpd and then run the **ntpdate command** to manually synchronize the time. You might need to run the ntpdate command several times until the time difference (or offset) is far less than 1 second. After manually synchronizing the time in this way, you can start the ntpd daemon again. This process is shown in the following output:

```
[root@server1 ~]# service ntpd stop
Shutting down ntpd:                                        [  OK  ]
[root@server1 ~]# ntpdate -u 0.fedora.pool.ntp.org
4 Sep 15:03:43 ntpdate[2908]: adjust time server 206.248.190.142 offset
0.977783 sec
[root@server1 ~]# ntpdate -u 0.fedora.pool.ntp.org
4 Sep 15:03:53 ntpdate[2909]: adjust time server 206.248.190.142 offset
0.001751 sec
[root@server1 ~]# ntpdate -u 0.fedora.pool.ntp.org
4 Sep 15:04:01 ntpdate[2910]: adjust time server 206.248.190.142 offset
0.001291 sec
[root@server1 ~]# service ntpd start
Starting ntpd:                                              [  OK  ]
[root@server1 ~]#
```

After restarting the ntpd daemon, you can use the **ntpq command** to see what actual time servers you are synchronizing with. Since time varies greatly by location, NTP uses a jitter buffer to store the difference between the same time measurements from different NTP servers. The jitter information is used by NTP when determining the most reliable time when several NTP servers are queried for time information. The `ntpq -p` command shows the offset and jitter in milliseconds, as shown here:

```
[root@server1 -]# ntpq -p
remote refid st when poll reach delay offset jitter
=======================================================================
ox.eicat.ca 139.78.135.14 2 u 6 64 3 28.662 11.138 0.046
adelaide.ph 142.3.100.15 3 u 2 64 3 62.211 30.870 0.574
one.trx.com 209.51.161.238 2 u 3 64 3 43.329 22.867 0.190
[root@server1 -]#
```

By default, the NTP daemon is not configured as an NTP server, since there is only a single NTP `restrict` line within the `/etc/ntp.conf` file:

```
restrict 127.0.0.1
```

This line allows your local client to query the NTP daemon for time information with no restrictions. If you want to allow other computers to query your NTP daemon (ntpd) for time information, simply edit the `/etc/ntp.conf` file again and add a line that identifies the specific computers or networks that are allowed to query your NTP daemon. For example, the following line within `/etc/ntp.conf` allows all computers on the 192.168.1.0 network to query your NTP daemon for time information but prevents other computers from modifying your NTP server configuration (**nomodify notrap**).

```
restrict 192.168.1.0 mask 255.255.255.0 nomodify notrap
```

![](img/c27875544958897d817484d558c208c8_614_0.png)

If you modify the `/etc/ntp.conf` file, you must restart `ntpd` for those changes to take effect.

### Working with chronyd

Some modern Linux distributions, such as Fedora 20, use `chronyd` in place of `ntpd`, since it offers a faster response time and is backwards-compatible with ntpd. It uses the `/etc/chrony.conf` configuration file, which has a format nearly identical to that of `/etc/ntp.conf`. You can add different NTP servers to query using the same syntax used within `/etc/ntp.conf`, as well as add lines that allow other NTP servers to query you on a particular subnet. Rather than using a `restrict` line to allow other NTP clients to query your time as seen earlier in `/etc/ntp.conf`, you can simply add the line **allow subnet** to `/etc/chrony.conf`. For example, the line **allow 192.168.1/24** would allow NTP clients to connect from the 192.168.1.0 network (with a 24-bit subnet mask of **255.255.255.0**).

For management, `chronyd` uses the **chronyc command** to provide the functionality that the `ntpq`, `date`, and `ntp` commands do with `ntpd`. For example, to view the servers that you are currently polling for time, simply run the `chronyc sources` command, as shown here:

```
[root@server1 -]# chronyc sources
210 Number of sources=4
MS Name/IP address       Stratum  Poll  LastRx   Last sample
================================================================
^ + 209.167.68.100       2      6     22       +11ms[ +11ms] +/-  87ms
^ + 66.102.79.92         2      6     32       +356us[ +3669us] +/- 62ms
^ + ox.eicat.ca          2      6     42       -431us[- 4198us] +/-  75ms
^ * 216.234.161.11       2      6     50       -41us[  +72us] +/-  81ms
[root@server1 ~]#
```

When run without arguments, the chronyc command provides an interactive chronyc> prompt that you can use to type additional commands. Typing help at the chronyc> prompt will display a list of commands, including polltarget (which can be used to poll a specified NTP server) and settime (which can be used to manually set the date and time to a specified value).

Nearly all desktop environments installed today obtain time from an Internet time server using NTP and allow for NTP client configuration using a graphical application. For example, to obtain time from an Internet time server using chrony on a Fedora 20 system, you can navigate to the Activities menu, Show Applications, Settings, Date & Time within the GNOME desktop to open the Date & Time utility shown in Figure 13-5.

![](img/c27875544958897d817484d558c208c8_615_0.png)

All system date information is calculated relative to the time zone that you selected during Linux installation. The configuration of each time zone is stored in the /usr/share/zoneinfo directory. If you need to manually change the zone following installation, you can use the tzselect command or set OFF next to Automatic Time Zone in Figure 13-5 and select your desired time zone.

# NIS

You can use the Network Information Service (NIS) to coordinate common configuration files, such as /etc/passwd and /etc/hosts, across several Linux computers within an organization. Each computer that participates in NIS belongs to an NIS domain and uses an NIS map for accessing certain information rather than use the local configuration files. Furthermore, you can configure a NIS master server to send all NIS map configuration to NIS slave servers, which then distribute these NIS maps to all other Linux computers, known as NIS clients. Alternatively, a master NIS server can send NIS map configuration directly to NIS clients.

![](img/c27875544958897d817484d558c208c8_615_1.png)
