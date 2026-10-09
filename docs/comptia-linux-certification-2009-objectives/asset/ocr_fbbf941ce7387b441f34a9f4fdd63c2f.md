# ## TOPIC E

# Maintain the System Time

In the previous topic, you scheduled jobs to run at a specific time. You need to monitor system clocks so that all systems show the same time. In this topic, you will maintain the system time.

Suppose you work in a company with clients in various cities around the world. You may need to synchronize your system time with that of your client’s time zone to enable easier business transactions.

# Network Time Protocol

Network Time Protocol (NTP) is a standard Internet protocol for synchronizing the internal system clock with the *true time* or the *average time* on a number of high accuracy clocks around the world. NTP is used for transmitting and receiving time on TCP/IP networks. NTP is also used to set the clock of one computer to match that of another and synchronize it with the network clock.

![](bbox=[0.08, 0.43, 0.45, 0.54])

![](bbox=[0.45, 0.43, 0.65, 0.54])

![](bbox=[0.08, 0.54, 0.45, 0.63])

*Figure 10-22: Synchronization of system clocks with network time using NTP.*

# Drift Files

The drift file is a file found in the `/etc/ntp` directory. The NTP drift file is used by the *ntpd* daemon to reset the time when the system is restarted. The drift file synchronizes the system clock and the clock drift to display the time from the NTP server.