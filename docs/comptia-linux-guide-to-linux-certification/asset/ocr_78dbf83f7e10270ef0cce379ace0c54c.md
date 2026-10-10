the systemctl command. The following command displays all Systemd services and their state (dead indicates that it is currently not running):

```
[root@server1 ~]# systemctl -a | grep service | less
abrt-ccpp.service       loaded active  exited    Install ABRT coredump
abrt-oops.service        loaded active  running   ABRT kernel log watcher
abrt-vmcore.service      loaded active  exited    Harvest vmcores for ABRT
abrd.service            loaded active  running   ABRT Automated Bug Repo
acpid.service            loaded active  running   ACPI Event Daemon
alsa-store.service       loaded inactive dead     Store Sound Card State
arp-ethers.service       loaded inactive dead     Load static arp entries
atd.service             loaded active  running   Job spooling tools
auditd.service            loaded active  running   Security Auditing
avahi-daemon.service      loaded active  running   Avahi mDNS/DNS-SD Stack
crond.service           loaded active  running   Command Scheduler
cups.service            loaded active  running   CUPS Printing Service
dbus-org.bluez.service  error inactive dead      dbus-org.bluez.service
dbus.service            loaded active  running   D-Bus System Message Bus
:
```

You can see detailed information about a particular Systemd daemon by using the status argument to the systemctl command. For example, systemctl status crond.service would show detailed information about the cron daemon.

To configure a Systemd daemon to start in the default target (e.g., graphical.target), you can use the enable argument to the systemctl command. For example, to ensure that the cron daemon is started at system initialization, you can run the systemctl enable crond.service command. Alternatively, the systemctl disable crond.service would prevent the cron daemon from starting when your system is booted.

The systemctl command can also be used to change between targets. You can switch to multi-user.target (which is analogous to runlevel 3) by running either the systemctl isolate multi-user.target or systemctl isolate runlevel3.target command. Alternatively, you can switch to graphical.target (which is analogous to runlevel 5) by running the systemctl isolate graphical.target or systemctl isolate runlevel5.target command.

# ## The X Windows System

So far in this chapter, we've focused on performing tasks using a BASH shell command-line interface obtained after logging in to a character terminal. Although most administrators favor the command-line interface, Linux users typically use GUIs for running user programs. Thus, you need to understand the components that make up the Linux GUI. In particular, you need to know how to start, stop, and configure them.

# ### Linux GUI Components

The Linux GUI was designed to function consistently, no matter what video adapter card and monitor are installed on the computer system. It is composed of many components, each of which works separately from the video hardware.