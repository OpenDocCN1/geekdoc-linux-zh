
## LAB 79
### Maintain System Time: NTP
**Lab Objective:**
Learn how to maintain system time and synchronize the clock with NTP.

**Lab Purpose:**
In this lab, you will learn about the classic Network Time Protocol (NTP) and its settings for synchronizing the system clock.

**Lab Tool:**
Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**
A single Linux machine, or virtual machine

**Lab Walkthrough:**
**Task 1:**
Open the Terminal and run: `sudo apt install ntp ntpdate`

Now view the main NTP configuration file with: `cat /etc/ntp.conf`

NTP works by synchronizing time in a tree topology—your lab machine gets its time from a distro-specific pool of servers, specified by “pool” (for example, `ubuntu.pool.ntp.org`). Ubuntu’s own servers get their times from some upstream source, and so on, all the way up to a system of atomic clocks in laboratories worldwide.

**Task 2:**
Now run:
- `sudo systemctl stop ntp.service`
- `sudo ntpdate ntp.ubuntu.com`

(You can, of course, use a different time server in place of `ntp.ubuntu.com`.)

After a few seconds, you should see output indicating that `ntpdate` has updated the system time, noting where it got the time from and what the offset adjustment was.

`ntpdate` can be useful for updating the system time on every boot, sometimes before `ntpd` (the NTP daemon) takes over, or for synchronizing the time manually on servers that usually have restricted or no internet access. Beyond that, however, `ntpd` is recommended instead of running `ntpdate` via `cron`.

**Notes**
`ntpq` is a command, mostly useful for debugging, that can be used to query NTP servers for various information.

## LAB 80
### Maintain System Time: Chrony
**Lab Objective:**
Learn how to maintain system time and synchronize the clock with Chrony.

**Lab Purpose:**
In this lab, you will learn about `chrony`, a newer implementation of NTP, and its settings for synchronizing the system clock.

**Lab Tool:**
Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**
A single Linux machine, or virtual machine

**Lab Walkthrough:**
**Task 1:**
Open the Terminal and run:
- `sudo apt install chrony`
- `sudo systemctl start chrony`

Now view the main Chrony configuration file with: `cat /etc/chrony/chrony.conf`

You should recognize some similarities with the NTP config file from Lab 79.

**Task 2:**
Now run `sudo chronyc`. You will find yourself at an interactive prompt. You can now experiment with the `chronyc` tool:
- `tracking`
- `activity`
- `ntpdata`

Run `help` at this prompt to see a list of what you can do, or run `quit` to quit.

In comparison with `ntpdate`, the chrony FAQ page states "If your computer is connected to the Internet only for a few minutes at a time, the network connection is often congested, you turn your computer off or suspend it frequently, the clock is not very stable (e.g. there are rapid changes in the temperature or it's a virtual machine), or you want to use NTP on an isolated network with no hardware reference clocks in sight, `chrony` will probably work much better for you."

**Notes:**
`hwclock` can be used to check the hardware time, which is not necessarily the same as system time (especially when the hardware clock uses a different timezone). Run `sudo hwclock` followed by `date`—do they match up?

The Chrony FAQ page URL is: `https://chrony.tuxfamily.org/faq.html#_how_does_code_chrony_code_compare_to_code_ntpd_code`

## LAB 81
### System Logging: Rsyslog
**Lab Objective:**
Learn how to configure the `rsyslog` logging daemon.

**Lab Purpose:**
In this lab, you will learn about basic configuration of `rsyslog` and its different logging options.

**Lab Tool:**
Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**
A single Linux machine, or virtual machine

**Lab Walkthrough:**
**Task 1:**
Open two Terminal windows/tabs.

In the first one, run: `tail -f /var/log/syslog`

In the second one, run: `logger "Hello World"`

Now go back to the first tab. Did your friendly message show up in the system logs? Hit `Ctrl+C` to exit `tail`.

> `logger` is a generic utility for sending logs to a number of daemons, including `rsyslog`, and `journal` which we will discuss in Lab 83.

**Task 2:**
Now look at the configuration:
```bash
grep -v -e ^# -e ^$ /etc/rsyslog.conf /etc/rsyslog.d/*
```

This may vary by distro—once you locate the correct file(s), you may want to open them with a text editor.

Ultimately, you are looking for a file such as `50-default.conf` or similar, defining what facilities log to what files. On Ubuntu, this file should contain a line like:
```
auth,authpriv.* /var/log/auth.log
```

At the top of this file, add the following line:
```
*.* /var/log/allthelogs
```

Then restart the daemon: `systemctl restart rsyslog`

Wait a few minutes (or create your own logs with `logger`), then check the contents of `/var/log/allthelogs`. This should be an amalgamation of all the logs which are going to many other log files.

**Task 3:**
Clean up by deleting the line you added to the `rsyslog` config, and run `systemctl restart rsyslog`

**Notes:**
Aside from `journald`, which most distros have migrated to as a result of Systemd, there are also other logging daemons like `syslog` and `syslog-ng`. While some daemons have their own configuration formats, all at least support the classic `syslog` configuration format (and that should be what you saw in `rsyslog`’s own configs). Learn that format, and you will have learned configuration for all of the major logging daemons.

## LAB 82
### System Logging: Logrotate
**Lab Objective:**
Learn how to configure `logrotate` to rotate system logs.

**Lab Purpose:**
`logrotate` is a commonly used tool to rotate logs, i.e. archive them every X days/weeks and delete them every Y weeks/months. In this lab, you will learn how to configure it.

**Lab Tool:**
Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**
A single Linux machine, or virtual machine

**Lab Walkthrough:**
**Task 1:**
Open the Terminal and run `cat /etc/logrotate.conf`

This is the main logrotate configuration file, the one that contains the default directives. You may see lines like:
```
weekly
rotate 4
create
```

In combination, these lines will save an archive of some log file every week, keep each archive for four weeks, and create a new empty log file after rotating an older one.

Additionally, you probably have a directory called `/etc/logrotate.d`, where some package-specific configs are stored. Ubuntu has one for `apt`, so look at `/etc/logrotate.d/apt`, or another file of your choosing.

You might see directives here like `rotate 12` (keep for 12 weeks instead of 4, or 12 months if it includes `monthly`), `compress` to compress the archives, or `notifempty` to ignore the log if it is empty.

See `man logrotate` for more details.

**Task 2:**
Now, with `sudo` (or `sudoedit`), open a text editor and create a file called `/etc/logrotate.d/mylog` with the following contents:
```
/var/log/mylog.log {
    hourly
    su root syslog
    rotate 2
    create
    compress
    missingok
}
```

Then: `sudo touch /var/log/mylog.log`

Normally you'd have to wait at least an hour to see any rotation happen, but you can force the situation with the `-f` switch. Run:
- `sudo logrotate -fv /etc/logrotate.d/mylog`
- `ls -al /var/log/mylog*`

You should see a compressed archive of the original file, as `mylog.log.1.gz`, and a new log called `mylog.log`. Run that first command twice more. The second time you run it will create a second archive file, but on the third run you should see a line at the bottom saying “removing old log /var/log/mylog.log.3.gz”, as per the configuration file.

**Task 3:**
Finally, clean up: `sudo rm /etc/logrotate.d/mylog /var/log/mylog*`

**Notes:**
Typically, `logrotate` is run via a daily `cron` job. Can you find where this `cron` job is configured on your system? (Hint: See Lab 75!)
