```
MS Name/IP address       Stratum  Poll  LastRx   Last sample
================================================================
^ + 209.167.68.100       2      6     22       +11ms[ +11ms] +/-  87ms
^ + 66.102.79.92         2      6     32       +356us[ +3669us] +/- 62ms
^ + ox.eicat.ca          2      6     42       -431us[- 4198us] +/-  75ms
^ * 216.234.161.11       2      6     50       -41us[  +72us] +/-  81ms
[root@server1 ~]# _
```

When run without arguments, the chronyc command provides an interactive chronyc> prompt that you can use to type additional commands. Typing help at the chronyc> prompt will display a list of command commands, including polltarget (which can be used to poll a specified NTP server) and settime (which can be used to manually set the date and time to a specified value).

Nearly all desktop environments installed today obtain time from an Internet time server using NTP and allow for NTP client configuration using a graphical application. For example, to obtain time from an Internet time server using chrony on a Fedora 20 system, you can navigate to the Activities menu, Show Applications, Settings, Date & Time within the GNOME desktop to open the Date & Time utility shown in Figure 13-5.

![](bbox=[0.14, 0.44, 0.29, 0.54])

All system date information is calculated relative to the time zone that you selected during Linux installation. The configuration of each time zone is stored in the /usr/share/zoneinfo directory. If you need to manually change the zone following installation, you can use the tzselect command or set OFF next to Automatic Time Zone in Figure 13-5 and select your desired time zone.

# NIS

You can use the Network Information Service (NIS) to coordinate common configuration files, such as /etc/passwd and /etc/hosts, across several Linux computers within an organization. Each computer that participates in NIS belongs to an NIS domain and uses an NIS map for accessing certain information rather than use the local configuration files. Furthermore, you can configure a NIS master server to send all NIS map configuration to NIS slave servers, which then distribute these NIS maps to all other Linux computers, known as NIS clients. Alternatively, a master NIS server can send NIS map configuration directly to NIS clients.

![](bbox=[0.14, 0.74, 0.92, 0.96])