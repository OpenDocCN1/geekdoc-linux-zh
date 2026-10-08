printer is ready, how many print jobs it has, and so on. The `stop` and `start` commands can stop a printer and start it back up. The printers shown depend on the printers configured for a particular print server. A printer configured on CUPS will only show if you have switched to CUPS.

```
# lpc
lpc> status myepson
myepson:
  printer is on device 'hal'  speed -1
  queuing is enabled
  printing is enabled
  1 entry in spool area
```

# ## lpq and lprstat

You can manage the print queue using the `lpq` and `lprm` commands. The `lpq` command lists the print jobs currently in the print queue. With the `-P` option and the printer name, you can list the jobs for a particular printer. If you specify a username, you can list the print jobs for that user. With the `-l` option, `lpq` displays detailed information about each job. If you want information on a specific job, simply use that job's ID number with `lpq`. To check the status of a printer, use `lprstat`.

```
# lpq
myepson is ready and printing
Rank   Owner  Jobs  File(s)            Total Size
active  chris    1   report              1024
```

# ## lprm

The `lprm` command enables you to remove a print job from the queue, erasing the job before it can be printed. The `lprm` command takes many of the same options as `lpq`. To remove a specific job, use `lprm` with the job number. To remove all print jobs for a particular printer, use the `-P` option with the printer name. `lprm` with no options removes the job that is currently printing. The following command removes the first print job in the queue (use `lpq` to obtain the job number):

```
# lprm 1
```

# ## CUPS Command Line Administrative Tools

CUPS provides command line administrative tools like `lpadmin`, `lpoptions`, `lpinfo`, `enable`, `disable`, `accept`, and `reject`. The `enable` and `disable` commands start and stop print queues directly, whereas the `accept` and `reject` commands start and stop particular jobs. The `lpinfo` command provides information about printers, and `lpoptions` lets you set printing options. The `lpadmin` command lets you perform administrative tasks like adding printers and changing configurations. CUPS administrative tools are listed in Table 26-4.