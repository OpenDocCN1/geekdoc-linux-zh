A better option for network time synchronization is to use the Network Time Protocol (NTP) to sync time with a network time provider. NTP manages time in a much cleaner fashion than netdate. NTP adjusts time in a much gentler manner. If there is a time differential between the time provider and the time consumer (your local system), it adjusts time gradually in small increments until time is eventually synchronized.

NTP is also widely supported by most operating systems. The netdate option only works with the time service on a Linux/UNIX time provider. NTP, on the other hand, allows time to be synchronized among systems in a heterogeneous network environment. It's supported by

+   * Linux
+   * Windows
+   * NetWare
+   * UNIX
+   * Etc.

NTP is a little more complex than netdate. Therefore, to implement NTP, you need to be familiar with the following:

+   * How NTP works
+   * Configuring the ntpd daemon
+   * Monitoring NTP operations

Let's begin by discussing how NTP works.

# How NTP Works

You can use the ntpd daemon on Linux to synchronize time with another NTP time provider. In fact, a system running ntpd can function as both a *time consumer* and a *time provider* at the same time. The NTP protocol operates over IP port 123. The time consumer sends a time synchronization request to the time provider on port 123. The time provider sends its time to the consumer, and the system time on the consumer is adjusted according to the NTP algorithm.

![](bbox=[0.05, 0.73, 0.15, 0.82])

Because NTP is designed to synchronize time across global networks, it assumes all systems involved are configured to use UTP time.

Several key NTP concepts that you need to be familiar with include the following:

+   * **Stratum** NTP uses the concept of *stratum* to define a hierarchy of NTP servers:
+     * **Stratum 1** Stratum 1 time servers get their time from a reference time source, such as the Naval atomic clock. (See tycho.usno.navy.mil for more information.)
+     * **Stratum 2** Time servers that get their time from stratum 1 servers