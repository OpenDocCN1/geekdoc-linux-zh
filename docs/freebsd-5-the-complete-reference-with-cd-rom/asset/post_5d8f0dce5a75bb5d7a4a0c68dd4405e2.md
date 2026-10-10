
this, though, the Internet’s available stratum 1 servers would quickly become overwhelmed by requests, and the entire system would collapse. In practice, therefore, it’s best to synchronize small networks’ main time server to stratum 2 servers. The reduction in accuracy is minor for most purposes, and this procedure helps spread the load across more servers. The usual cutoff point between “small” and “large” networks for this purpose is roughly 100 computers.

To locate a suitable stratum 2 server, consult `http://www.eecs.udel.edu/~mills/ntp/clock2.html`. This site maintains a list of many public stratum 2 servers (157 sites as I write). Locate a server that’s near you and make note of its hostname or IP address for the procedure outlined in the upcoming section, “Configuring an NTP Server.” Many sites request that you contact them before you synchronize off of them. If your selected site is one of these, be sure to do so as a courtesy to the server’s operators.

> Because the *measurement error* involved in NTP is related to packet latencies, your parent time server should produce low ping times. Try pinging some potential parent servers to discover which ones are best.

In addition to the public stratum 2 servers, you may have access to other servers. For instance, many ISPs operate time servers that are accessible to customers. Such servers are typically close to customers’ systems, and are good choices in terms of producing low latencies.

Unfortunately, NTP servers aren’t always accessible. Network paths may go down, or a server may discontinue operation altogether. Potentially worse, the server may be synchronized to a poor clock source. For this reason, a common practice is to synchronize your network’s primary NTP server to multiple external NTP servers. Three external servers are typically enough. The `ntpd` program can then detect if one server is bad and automatically disregard its time signals. Using multiple external NTP servers may be overkill for a small network, though. In the event of a transient problem, `ntpd` can keep your clock going with little loss of accuracy, because it tracks the deviation of your system’s clock from an accurate time source and can compensate even if access to the accurate time source is lost.

Whether you synchronize your primary time server to one external server or several, you should synchronize all of your network’s other systems to your one primary server. If you’ve got a network of 50 computers, this practice can greatly ease the load on external time servers, with very minor detriment to the accuracy of your local systems’ clocks. Large organizations may operate two or more local time servers for redundancy and synchronize local clocks to all local servers.

## Configuring NTP

FreeBSD provides two options for NTP use. The first is to use `ntpdate`, an NTP client program, to set the computer’s clock whenever you boot the computer. The second option is to use the full `ntpd` package to continuously monitor and adjust the computer’s clock, and optionally to serve time to other computers.

### Setting the Clock at Boot Time

If you frequently reboot your computer, you can set its clock at boot time and the clock will remain reasonably accurate. You can activate this configuration using sysinstall:

-   1. As root, type `/stand/sysinstall` to start the configuration tool.
-   2. Select **Configure** to get to the FreeBSD Configuration Menu.
-   3. Select **Networking** to get to the Network Configuration Menu.
-   4. Select **Ntpdate** to activate the ntpdate option. The system presents the NTPDATE Server Selection menu, which lists many NTP server sites, mostly from the list of stratum 2 servers mentioned in “Locating Parent Time Servers.”
-   5. Select a server from the list. (Later, you can change it to one that’s not on the list, as described shortly.) sysinstall returns to the Network Configuration Menu.
-   6. Pick the **Cancel**, **Cancel**, and **Exit Install** options to quit from sysinstall.

These steps add lines such as the following to your `/etc/rc.conf` file:

```text
ntpdate_flags="clock-2.cs.cmu.edu"
ntpdate_enable="YES"
```

If you prefer, you can add these lines manually rather than using sysinstall. You can also change the server listed in the `ntpdate_flags` option if you prefer to use a server that’s not on the preconfigured list. For instance, you would edit this option for a computer other than your primary time server; you would list your local primary time server.

When you next boot the computer, FreeBSD will contact the server you specified and use ntpdate to synchronize its time to the server’s time. If you’re not running ntpd, you can do the same thing at any time after the system has booted by typing `ntpdate server-name`, where `server-name` is the hostname of the NTP server. You could put such a command in a cron job (described in Chapter 6) to set the time once a day, for instance, if you can tolerate the potential for a few seconds’ drift over a day.

### Configuring an NTP Server

To implement more continuous time adjustment, you must activate the ntpd server. Two steps are required: You must edit the `/etc/rc.conf` file to have FreeBSD start ntpd at boot time and you must edit the `/etc/ntpd.conf` file with the options you want to enable, including the time server to be used.

To activate ntpd at boot time, add the following line to `/etc/rc.conf`:

```text
xntpd_enable="YES"
```

When you reboot the computer, the server will activate, contact its parent servers, and begin adjusting your clock on a fine scale to keep it as accurate as possible. Once you finish configuration, you can activate the server manually by typing `ntpd` as root.

Actually configuring **ntpd** requires editing its configuration file, `/etc/ntp.conf`. The most important option appears near the start of the file:

```text
server clock-2.cs.cmu.edu
```

This line tells the system what NTP server to use as its parent. You may include several such lines, one for each server, and **ntpd** will contact them all and use the most accurate source from the set. In fact, a default configuration includes a reference to 127.127.1.0, which is an IP address that **ntpd** associates with the local clock, as a fallback should all other servers be unavailable. (Another line beginning with the keyword *fudge* gives this local clock a stratum of 10, so it won't enter into the picture if a real server is available.)

If you want to configure an entire network to use NTP, you should set up one computer to access one or more external NTP servers. You can then use the same configuration on internal computers, except that they should point to the primary local NTP server *only*. The primary server takes on a stratum one higher than the one to which it synchronizes, and the rest of the systems are one stratum higher. For instance, if your primary computer synchronizes to a stratum two server, then it's a stratum 3 server, and the rest of your systems are stratum 4 servers (although they may have no clients).

Unfortunately, it's not always easy to tell if **ntpd** is working as you expect. The server often doesn't adjust the time all at once; instead, it may *slow* the clock, meaning that it adjusts the rate at which it runs until the clock's time is accurate. The server may also abort completely if the clock is off by over an hour. You can check that the server is running by typing `ps ax | grep ntpd`, but to see if it's working correctly, you may need to use a monitoring program called **ntpq**. This program has many advanced options, but the most basic is the `peers` command, which you type at its **ntpq** prompt. Figure 22-1 shows this program in action. The server whose name is marked with an asterisk in the leftmost column is the one to which **ntpd** has synchronized its clock. Servers marked

![](img/f34d37e3abe9f4517128e54f80ab2616_576_0.png)

Figure 22-1. The **ntpq** program provides a way to monitor the behavior of the **ntpd** server.
