enables your server to weed out any servers that deliver a bad time signal, and it also gives automatic fallback in case an upstream server becomes temporarily or permanently unavailable. If your NTP server won’t be serving many computers often, you may want to configure it for three servers initially and then drop the ones your system isn’t using as its primary time source after a day or two. This will reduce the load on these servers.

You may want to peruse your configuration file for entries to remove. For instance, the configuration file may contain references to servers you’d rather not use or other odd options with associated comments that make them think they’re inappropriate. Generally speaking, you shouldn’t adjust entries in the ntp.conf file other than the reference server lines, but special circumstances or odd starting files may require you to make changes.

Once you’ve made your changes, start or restart your NTP daemon. Typically, this is done via a SysV startup script:

```
# /etc/init.d/ntp restart
```

You may need to change the path to the file, the SysV script filename, or the option (change restart to start if you’re starting NTP for the first time). Most distributions configure NTP to start whenever the system boots once you install the server. Consult Chapter 4 for details on changing this configuration.

To verify that NTP is working, you can use `ntpq`, which is an interactive program that accepts various commands. Figure 10.2 shows it in operation, displaying the output of the `peers` command, which summarizes the servers to which your NTP server is connected. (Typing `ntpq -p` causes the program to display this list and then exit.) In Figure 10.2, three external servers are listed, plus LOCAL(0), which is the last-resort reference source of the computer’s own clock. The `refid` column shows the server to which each system is synchronized, the `st` column shows the stratum of the server, and additional columns show more technical information. The server to which yours is synchronized is denoted by an asterisk (*), other servers with good times are indicated by plus signs (+), and most other symbols (such as x and –) denote servers that have been discarded from consideration for various reasons. Consult ntpq’s man page for more information about its operation.

# FIGURE 10.2 The ntpq program enables you to verify that an NTP server is functioning correctly.

![](bbox=[0.22, 0.72, 0.78, 0.885])