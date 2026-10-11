If **ntpd** is started and a drift file exists, the daemon adjusts the clock relative to the drift rates in the file and begins functioning normally. Over time, the file becomes more accurate as the nuances of the clock's frequency error are better known.

![](bbox=[0.08, 0.15, 0.18, 0.25])

If you start your NTP daemon and the system is more than 1,000 seconds out of correct time, the **ntpd** daemon errors out and the clock must be set by hand.

You can set the system time with the `date` command, and the hardware clock time can be set with the following command:

```sh
hwclock --hctosys
```

This sets your system clock to the value in the hardware clock, hopefully bringing it close enough to the real time that the **ntpd** daemon can take over from there.

# ## Setting Up NTP

To determine whether the NTP package is currently installed, on an RPM-based system, use the command shown here:

```sh
rpm -q ntp
```

If you receive output that is similar to the following, the NTP package is installed:

```sh
ntp-4.1.1-1
```

Then you can edit the `/etc/ntp.conf` file to set the time sources; usually you need at least one line in the file to have a functional **ntpd** daemon:

```sh
server tar.foo.net
```

![](bbox=[0.08, 0.61, 0.18, 0.71])

Be very conscious of the protocols of using someone else's time server for reference. It's considered impolite to just latch onto someone else's time server, and it's almost guaranteed to get you blacklisted or put in someone's denied file. Check out the Public NTP Time Servers page (and read the whole thing!) at [http://www.eecs.udel.edu/~mills/ntp/servers.html](http://www.eecs.udel.edu/~mills/ntp/servers.html).

You might need an **ntp.drift** file, but that is created by the **ntpd** daemon itself, so listing it in the configuration file might not be necessary. However, it is a good idea to put a second line in the file that matches the following:

```sh
driftfile /etc/ntp.drift
```

You just need to restart the **ntpd** daemon to begin using NTP at this point. On a Red Hat machine, you would type

```sh
service ntpd restart
```

If you don't want to use the **ntpd** daemon, you can use the **ntpdate** command to manually set the time from an authoritative source, such as