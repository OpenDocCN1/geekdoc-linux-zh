Following the syntax discussed earlier, the combination of this command and the information that Samba replaces for `%p` and `%s` (printer and data stream, respectively) provides the final touch to the Samba print configuration. After this edit is complete, stop and start both the lpd daemon and Samba itself:

```
```text
/etc/rc.d/init.d/lpd stop
/etc/rc.d/init.d/lpd start
/etc/rc.d/init.d/samba stop
/etc/rc.d/init.d/samba start
```
```

At this point, Windows clients will be able to connect to the raw print queue just like they connect to any other shared printer. Refer to Windows’s documentation for details on printer connection and networking instructions.

# MANAGING PRINT QUEUES

As an administrator of a Linux server, you must have the capability to enforce a certain amount of control over your print system. This control goes beyond simple settings for maximum print job sizes—it goes into actual queue management and troubleshooting, both of which are primarily administrative tasks (although some things can be done at a user level).

LPRng provides what are considered to be traditional BSD style queue administration tools: `lpq`, `lprm`, and `lpc`.

> **Note**
> 
> Those who are more familiar with SysV print systems will note the lack of such items as `lpadmin` and `lpstat`. Odds are, however, that by using combinations of `lpq`, `lprm`, and `lpc`, you will find functionality similar to that of these utilities.

# PEEKING INTO QUEUES WITH lpq

The lpq utility is rather simple in nature. It merely produces a printout of the latest status of a print queue. If jobs are stacked up, it shows which jobs are there and what each job’s number is, as well as its position in the queue (see Listing 31.9).

# LISTING 31.9  OUTPUT FROM lpq—ONLY ONE QUEUED PRINT JOB

```
```text
1  [erat@rumble ~]$ lpq
2  Printer: lp@rumble 'PostScript'
3  Queue: 1 printable job
4  Server: pid 716 active
5  Unspooler: pid 717 active
6  Status: printed all 670 bytes at 09:24:07
7  Rank  Owner          Job  Files          Class  Size  Time
8  active erat@rumble+715  A  715 /etc/printcap  670 09:24:07
9  [erat@rumble ~]$
```
```

In line 2, you see that the information listed pertains to the lp print queue in /etc/printcap (also known as PostScript, which means that the title of the printcap entry contains at least

![](bbox=[0.938, 0.334, 1.0, 0.452])