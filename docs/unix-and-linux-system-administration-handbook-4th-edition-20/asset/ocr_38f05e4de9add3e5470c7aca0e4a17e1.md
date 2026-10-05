# sendmail testing and debugging

on page 490. These changes can be made permanent with the sysctl command or by putting the appropriate echo commands in a shell script that runs at boot time.

For example, to change TCP's FIN timeout value, you could use the following command:

```
linux$ sudo sh -c "echo 30 /proc/sys/net/ipv4/tcp_fin_timeout"
```

Solaris and HP-UX use the ndd command to tune network parameters. The HP-UX implementation is well documented, and ndd-h (help) gives a clear description of each variable, its range of values, and the default value. Solaris's ndd understands a question mark to mean you want documentation, but you must backslash it (ndd?) to protect it from the shell. Unfortunately, Solaris's ndd names the tunable variables instead of describing them.

For example, to change the FIN timeout value with ndd on HP-UX,

```
hp-ux$ sudo ndd -set tcp_fin_wait_2 30000
```

The time unit for ndd is milliseconds, thus 30000 instead of 30. In Solaris, the variable is called tcp_fin_wait_2_flush_interval, with no units in the man page—but Google! In fact, the units are milliseconds, with the default value 675,000. ndd is described in more detail in Chapter 14, TCP/IP Networking on page 498 for Solaris and page 504 for HP-UX.

AIX uses no command to tune network parameters. sudo no -L lists tunable variables with their min, max, and current values with all these values. If you want a to be permanent, use no with the -p flag—your changes will survive a reboot.

For example, to set the TCP FIN_WAIT parameter, use

```
aix$ sudo no -p -o tcp_finwait=2
```

The units are half-seconds, so the value 60 achieves the 30 seconds recommended in the tuning table above no is also discussed on page 507.

# 20.13 SENDMAIL TESTING AND DEBUGGING

m4-based configurations are to some extent tested. You probably won't need to do low-level debugging if you use them. The debugging flags cannot test your design. While researching this chapter, we found errors in several of the configuration files and designs that we examined. The errors from invoking a feature without the prerequisite macro (e.g., using masqueraded_envelope without masquerading with MASQUERADE_AS) to total conflict between the design of the sendmail configuration and the firewall that contained whether and under what conditions was met

+   1. If you try this in the form sendmail echo 30 /proc/sys/net/ipv4/tcp_fin_timeout, you will generate a "permission denied" message—your shell attempts to open the output file before it runs sudo. Use the sudo to apply both the echo command and redirection. Ergo, you must create a root shell in which to execute the entire command: sudo sh -c "echo..."