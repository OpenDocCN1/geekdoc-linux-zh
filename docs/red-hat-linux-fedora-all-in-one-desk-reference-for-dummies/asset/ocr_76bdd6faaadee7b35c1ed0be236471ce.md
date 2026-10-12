# Controlling the print queue

The first field of the output shows the name of the queue with a job number appended to it (that number identifies the print job). You need that job number to cancel the print job.

To see the names of printers connected to your system, use the `lpc status` command. On my system, the `lpc status` command shows the following:

```
```
lpc status
HPLaserJetRoom210:
    printer is on device 'parallel' speed -1
    queuing is enabled
    printing is enabled
    no entries
    daemon present
```
```

Notice that queuing and printing are both enabled for this printer. The last line tells you that the `cupsd` daemon (a server that runs all the time) is running and available to handle print jobs.

You can use the `accept` and `reject` commands to enable or disable queuing for a print queue. For example, to stop queuing further print jobs for the `HPLaserJetRoom210` printer, I type

```
```
reject HPLaserJetRoom210
```
```

This command disables queuing jobs for this printer. If anyone tries to send a print job using the `lp` command, the user receives an error message like this:

```
```
lp: unable to print file: server-error-not-accepting-jobs
```
```

If you want to allow queuing of print jobs, but want to start or stop the printing, use the `enable` and `disable` commands. When you disable printing, users can submit print jobs, but nothing gets printed until you enable printing again. For example, here is the command I use to disable printing on the `HPLaserJetRoom210` printer: `disable HPLaserJetRoom210`

![](bbox=[0.15, 0.88, 0.25, 0.98])

If you're trying to print, but nothing seems to be coming out of the printer, check the printer status with the `lpc status` command and make sure that the `cupsd` scheduler is present and that both queuing and printing are enabled. To allow the queuing of print jobs, use the `accept` command and to start printing, use the `enable` command.