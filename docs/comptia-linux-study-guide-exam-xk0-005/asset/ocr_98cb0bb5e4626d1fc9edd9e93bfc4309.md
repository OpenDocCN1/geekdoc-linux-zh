| Runlevel | Description |
| :------- | :---------- |
| 4 | Custom. |
| 5 | Multiuser mode with GUI available. |
| 6 | Reboot the system. |

Note that runlevels 0 and 6 are not runlevels by definition. Instead, they denote a transition from the current system state to the desired state. For example, a running system currently operating at runlevel 5 is transitioned to a powered-off state via runlevel 0.

# **TABLE 6.10** Debian-based distribution SysV init runlevels

| Runlevel | Description |
| :------- | :---------- |
| 0 | Shut down the system. |
| 1 | Single-user mode used for system maintenance. |
| 2 | Multiuser mode with GUI available. |
| 6 | Reboot the system. |

To determine your system's current and former runlevel, you employ the `runlevel` command. The first number or letter displayed indicates the previous runlevel (N indicates that the system is newly booted), and the second number indicates the current runlevel. An example is shown in Listing 6.18 of a newly booted Red Hat-based SysV init system, which is running at runlevel 5.

```
**Listing 6.18 Employing the `runlevel` command**

```
# runlevel
N 5
#```
```

Instead of using a default target like systemd, SysV init systems employ a configuration file, `/etc/inittab`. This file used to start many different services, but in later years is only started terminal services and defined the default runlevel for a system. The file line defining the default runlevel is shown in Listing 6.19.