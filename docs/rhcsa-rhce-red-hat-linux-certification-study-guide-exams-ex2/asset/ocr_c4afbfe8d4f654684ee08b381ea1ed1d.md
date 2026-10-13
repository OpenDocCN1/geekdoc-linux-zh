I cite the man page, as it’s an excellent reference for the command required to create a report, while on the job, or even during a Red Hat exam. As with many other commands, this can be found in the EXAMPLES section. While the **-d** is associated with the **sadf** command, the double-dash (**--**) points to options associated with the **sar** command. So the **-r** reports memory usage, and the **-n DEV** reports statistics from network devices.

Of course, there are other important **sar** command switches. Those which may be relevant when you prepare a report on “processor, memory, disk, and network” utilization are described in Table 17-3.

With the switches listed in Table 17-3, you might modify the previous **sadf** command to meet all four of the items listed in the related RHCE objective:

```
```
# sadf -d /var/log/sa/sa21 -- -u -r -p -n DEV
```
```

In other words, the **sadf** command specifies output usable by a database (**-d**) from the database file in the */var/log/sa* directory associated with the twenty-first of the month. The double dash (**--**) points to **sar** command switches, with CPU utilization (**-u**); RAM utilization (**-r**); activity by block device; presented in more familiar block files such as sda (**-p**); with statistics from network devices (**-n DEV**).

| TABLE 17-3 |
| System Utilization Switches for the sar Command |
| Switch | Description |
|---|---|
| -d | Lists activity by block device, normally used with -p to specify common drive device filenames such as sda and sdb. |
| -n DEV | Reports statistics from network devices. |
| -p CPU | Lists statistics on a per-processor (or core) basis; e.g., -p CPU 0 specifies the first CPU. |
| -r | Reports memory utilization statistics. |
| -S | Collects swap space utilization statistics. |
| -u | Sets up a CPU utilization report, including categories related to applications executed at the user and system levels, idle time, and more. |
| -W | Reports swap statistics. |