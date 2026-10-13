# Automatic shutdown on power failure

If you use an uninterruptible power supply (UPS) to provide backup power for your system, you can use init to shut down the system gracefully when your UPS power is nearly drained. The default /etc/inittab includes the following line:

```
pf::powerfail:/sbin/shutdown -f -h +2 "Power Failure; \
System Shutting Down"
```

This line tells init to run shut down in case of a power failure. The powerfailaction is activated when a UPS program or powerd (a power monitoring daemon) sends the SIGPWR signal to init. The default setting allows the system to run on UPS power for two minutes before it halts. If your UPS is capable of sustaining power for a greater or lesser length of time, you should modify this value.

Because it is quite possible for power to come back before your UPS power is reasonably drained, init can be called to cancel a previously scheduled shutdown event. This is done using the following line in /etc/inittab:

```
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; \
Shutdown Cancelled"
```

When init receives a SIGPWR signal, and a file called /etc/powerstatus contains an OK string, the powerokwait action is activated.

# Managing init Files

As you already know, System V init uses a lot of files, symbolic links, and directories. To simplify management of init files, a few tools are available. This section discusses two such commonly used tools.

# Using chkconfig to manage run levels

The chkconfig utility enables you to maintain the various symbolic links necessary for starting and stopping services in a run level. This utility can manage run level configuration for all the scripts in the /etc/rc.d/init.d directory. Its uses are described next.