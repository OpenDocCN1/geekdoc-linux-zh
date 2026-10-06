
# Configuring NTP Servers

When you're setting up a network to use NTP, select one system (or perhaps two for a network with dozen or more computers) to function as the primary NTP server. Your computer needn't be very powerful, but it must have always-access to the Internet. You can install the NTP server and configure it.

Most Linux distributions ship the NTP software in a package called ntp or ntpd. Look for this package, and if it's not already installed, install it. If you can find this package, check http://www.ntp.org/downloads.html. This site hosts NTP source code, which you can compile and install. If you don't install your distribution's NTP package, you will need to create your own SysV startup script or start the NTP daemon in some other way.

Once NTP is installed, look for its configuration file, /etc/ntp.conf. This file contains various NTP options, but the most important are the server lines:

```
server clock.example
server ntp.pangeea.com
server time.luna.com
```

Each of these lines points to a single NTP server. When your local NTP daemon starts up, it connects all the servers specified in /etc/ntp.conf, measures their accuracy against each other, and settles on one as its primary source. Typically, you list about three upstream servers for a system that enables you to weed out any servers that deliver a bad time, and it gives you automatic fallback in an upstream server becomes temporarily or permanently unavailable. If your NTP server is not serving many computers itself, you may want to configure it for three servers initially and then drop the system you's not using as its primary source after a day or two. This will reduce the load on your servers.

You may want to purge your configuration file for entries to remove. For instance, the configuration file may contain references to servers you'd not use or other options with comments that make you think they're inappropriate. Generally speaking, you shouldn't adjust entries in the ntp.conf file other than the reference server lines, special configurations or default files may require you to make changes.

Once you've made your changes, start or restart your NTP daemon. Typically, this is done via a SysV startup script:

```
# /etc/init.d/ntp restart
```

You may need to change the path to the file, the SysV script filename, or the option (change restart to start) whenever starting NTP for the first time. Most distributions configure Chapter 5, “Booting Linux and Editing Files,” for details of changing this configuration.

To verify that your NTP is working, use ntp, which is an interactive program that accepts various commands. Figure 7.2 shows it in operation, displaying the output of the peers command, which displays the servers to your NTP server is connected. In Figure 7.2, three external servers are listed, plus LOCAL(0), which is the last-reference source of your computer's clock. The refid column shows the server to which each

# Maintaining the System Time

system is synchronized, the st column shows the stratum of the server, and additional columns show more technical information. The server to which yours is synchronized is denoted by an asterisk (*), other servers with good times are indicated by plus signs (+), and other symbols (such as x and -) denote servers that have been discarded for various reasons. You can obtain a list by passing -p or -peers to ntpq, as in ntpq -p, using an interactive mode. Console ntpq is man page for more information about its operation.

# FIGURE 7.2 The ntpq program enables you to verify that an NTP server is functioning correctly.

```
ntpq
remote peers      refid             st reach poll delay  offset Jitter
=====================================================================
clock,example.c 128.227.205.3      2   186 377  23.016 -0.624 10.787
tppega.de       172.21.152.1      2   186 377  41.664  0.018 1.528
time,luna       18.145.0.30      10   186 377  20.183 -0.223 0.366
ntpq            LOCAL(0)          10   186 377   0.000  0.000 0.001
```

You won't see a server as the source until a few minutes after you restart the NTP daemon. The reason is that your local NTP process takes a while to determine which of the sources is providing the best signal.

# Configuring NTP Clients

Once you've configured one or more NTP servers, you can configure the rest of your computers to point to them. The configuration is done just with a couple of exceptions:

- You set your NTP clients to refer to the NTP server (or servers) you've configured rather than to an outside NTP source. This way, your local systems won't put an unnecessary burden on the outside NTP server you've selected.
- You want to ensure that your NTP clients can't be accessed as servers. This is a security measure. You can do this with an iptables rule or using the restrict default ignore line in ntpq.conf. This line tells the server to ignore all incoming NTP requests. Ideally, you should use both methods.

Once you've configured a client, restart your NTP daemon. You can then use ntpq to check its status. You should see that it refers only to your network's own server. These systems should be listed as belonging to a stratum with a number higher than the servers to which they refer.

# Chapter 7 • Administering the System

In some cases, a simpler way to set the time on a client is to use ntpdate. This program is part of the NTP suite, and performs one-time clock setting. To use it, type the command name followed by the hostname or IP address of NTP server:

```
# ntpdate clock.example.com
```

Some NTP packages include a call to ntpdate in their startup scripts in order to ensure that the system is set to the correct time. The ntpdate command has been deprecated and could disappear from the NTP package at any time. Instead, you can start ntpdate with its -g option, which enables it to perform clock setting to a value that's wildly different from the current time (ordinarily, ntpdate exits if the system time differs by more than five minutes.)

# Serving Time to Windows

If your network hosts both Linux and Windows, you may want to use a Linux system as time source for Windows or use a Windows server as time source for Linux. One way to do this is to run NTP on Windows. Consult http://www.meinberg.org/english/ntp.htm or perform a search to locate NTP software for Windows. For Windows 2000/XP/Vista, you can type the command, where time.server is the name of your local NTP server. This command performs one-time setting of the clock but doesn't run in the background like the NTP package does. For older Windows 9x/Me, you can type to have the system time maintained by a Windows or Samba file or print the server.

# Running Jobs in the Future

Some maintenance tasks should be performed at regular intervals and are highly automated. For instance, the /tmp directory holds temporary files created by many users may want to delete. Linux provides a means of scheduling tasks to run at specified times. This tool is the cron program, which runs as cron jobs. A related tool is at, which enables you to run a command on one-time basis in the future as opposed to doing so on a regular basis, as cron does.

# Understanding the Role of cron

The cron program is a daemon, it runs continuously, looking for events that cause it to spring into action. Unlike most daemons, which are network servers, cron responds to temporal events. Specifically, it "wakes up" once a minute, examines configuration files in the /var/spool/cron and /etc/cron.d directories and the /etc/crontab file, and executes commands specified by these configuration files if it matches the time listed in the files.

There are two types of cron jobs: system cron jobs and user cron jobs. System cron jobs run as root and perform system-wide maintenance tasks. By default, most Linux distributions include system cron jobs that clean out old log rotations (as described in "Rotating Log Files"), and so on. You can add to this repertoire. Ordinary users can create user jobs, which might run user program on a regular basis. You can also create a user cron job as root, which might be handy if you need to perform some task not supported by the system cron jobs, which are scheduled rather rigidly.

One of the critical points to remember about cron jobs is that they run unsupervised. Therefore, you shouldn't call any program in a cron job if that program requires user input. For instance, you don't run a text editor in a cron job, but you might run a script that automatically manipulates text files, such as log files.

# Creating System Cron Jobs

The /etc/crontab file controls cron jobs. This file normally begins with several lines that set environment variables, such as PATH and MAILTO (the former sets the path, and the latter is the address to programs' output is mailed). The file contains several lines that resemble the:

```
0 4 * * * root-parts /etc/cron.daily
```

This line gives five fields that specify the time. The fields are, in the minute (0–59), the day of the month (1–31), the month (1–12), and the day of the week (0–7; both 0 and 7 correspond to Sunday). For the month and day-of-the-week values, you can use the first three letters of the name rather than a number, if you like.

> A useful mnemonic for the time fields is that the first four are ordered in increasing size. The day of the week doesn't fit neatly within this pattern and so is placed outside of that, in the fifth field.

In all cases, you can specify multiple values in several ways:

- An asterisk (*) matches all possible values.
- A list separated by commas (such as 0,6,12,18) matches any of the specified values.
- Two values separated by a dash (--) indicate a range, inclusive of the end points. For instance, 9–17 in the hour field specifies a time from 9:00 a.m. to 5:00 p.m.
