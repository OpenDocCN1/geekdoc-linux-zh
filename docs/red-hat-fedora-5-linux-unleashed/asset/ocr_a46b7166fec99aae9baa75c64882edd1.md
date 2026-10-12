Not all the output is shown here, but as you can see, chkconfig can display the value of off or on for each service and each runlevel. The sample output shows only those services that are started in runlevel 5. The chkconfig command can be used to reassign start or stop values for each runlevel and each service. As an example, to alter the scripts to start power management (controlled by the apmd script under /etc/rc.d/init.d) when using Fedora during runlevel 5, use chkconfig like this:

```
```
# chkconfig --level 5 apmd on
```
```

You can then verify this action by again using grep on chkconfig's output like this:

```
```
# chkconfig --list | grep apmd
apmd            0:off   1:off   2:on    3:on    4:on    5:on    6:off
```
```

The chkconfig command does not start or stop a service; instead, it alters the scripts that start or stop a service, or it can report on the status of a service. Affecting only the current runlevel by default, other runlevels can be modified by using the `-levels` option. You would use the `ntsysv` or `service` commands or run the daemons directly in order to actually start or stop services (as described later in this chapter). All these tools have useful man pages to refresh your memory of all the available options.

`ntsysv` is a graphical interface you can use to access `chkconfig` and use a graphical interface. `ntsysv` is an `ncurses`-based interface, meaning that it offers crude, block graphics and elements you can tab through and select by pressing the spacebar (see Figure 15.1).

![](bbox=[0.13, 0.55, 0.77, 0.88])

**FIGURE 15.1** The `ntsysv` utility only manages which services are started in the current runlevel. Use the `--level` option to modify other runlevels.