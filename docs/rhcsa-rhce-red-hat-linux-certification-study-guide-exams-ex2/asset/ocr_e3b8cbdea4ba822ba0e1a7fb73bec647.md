are straightforward. As just suggested in the previous section, the following commands are one way to shut down and reboot a system, respectively:

```
# init 0
# init 6
```

As with many things in Linux, there is more than one way to shut down and reboot a system. In fact, the commands associated with those very actions serve the purpose:

```
# shutdown
# reboot
```

# Upstart Replaces SysVinit

As Upstart is designed as a “drop-in” replacement for the older SysVinit system, in one way, not much has changed. But the way these first files are organized has changed greatly. As you might expect, the Upstart system is associated with the upstart package. To see the files installed with that package, run the following command:

```
# rpm -ql upstart
```

Review this list of files. It starts with a connection to the ConsoleKit, which (among other things) tracks user interaction with administrative tools. It continues with a message bus connection to the files in the /etc/init directory, as defined by the init-system-dbus.conf file. It then includes those runlevel control commands that you should be familiar with, as shown in Table 5-3.

TABLE 5-3 Runlevel Control Commands

| Command | Description |
|---|---|
| halt | Moves to runlevel 0, which shuts down the system |
| init | Manages the current runlevel (different from the init daemon) |
| initctl | Controls the init daemon |
| poweroff | Moves to runlevel 0, which shuts down the system |
| runlevel | Lists current and previous runlevel |
| telinit | Manages the current runlevel |