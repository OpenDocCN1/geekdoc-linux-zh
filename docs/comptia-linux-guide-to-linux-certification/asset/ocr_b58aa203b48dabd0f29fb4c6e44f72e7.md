![](bbox=[0.16, 0.07, 0.84, 0.28])

**Figure 10-1** The print process

An example of this process for a printer called `printer1` is illustrated in Figure 10-1. To see a list of all printers on the system and their status, you can use the `-t` (total) option to the `lpstat` command, as shown in the following output:

```
[root@server1 ~]# lpstat -t
scheduler is running
system default destination: printer1
device for printer1: parallel:/dev/lp0
printer1 accepting requests since Thu 26 Aug 2015 08:30:AM EDT
printer printer1 is idle. enabled since Thu 26 Aug 2015 08:42:23 AM EDT
[root@server1 ~]#
```

The preceding output indicates that there is only one printer on the system, called `printer1`, that it prints to a printer connected to the first parallel port on the computer (`parallel:/dev/lp0`) and that there are no print jobs in its print queue. In addition, the CUPS daemon (`scheduler`) is running and accepting jobs into the print queue for this printer. Also, the CUPS daemon sends print jobs from the print queue to the printer because the printer is enabled.

You can manipulate the status of a printer using either the `cupsaccept`, `cupsreject`, `cupsenable`, or `cupsdisable` command followed by the printer name. Thus, to enable spooling and disable printing for the printer `printer1`, you can use the following commands:

```
[root@server1 ~]# cupsaccept printer1
[root@server1 ~]# cupsdisable printer1
[root@server1 ~]# lpstat -t
scheduler is running
system default destination: printer1
device for printer1: parallel:/dev/lp0
printer1 accepting requests since Thu 26 Aug 2015 08:51:21 AM EDT
printer printer1 disabled since Thu 26 Aug 2015 08:51:21 AM EDT – Paused
[root@server1 ~]#
```

Any print jobs now sent to the printer `printer1` are sent to the print queue but remain in the print queue until the printer is started again.