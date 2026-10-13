# Table 25-2: CUPS Print Clients

| Printer Management | Description |
|---|---|
| `lprm options print job-id or printer` | Removes a print job from the print queue. You identify a particular print job by its number as listed by `lpq`. `-P printer` removes all print jobs for the specified printer. |
| `lpc` | Manages your printers. At the `lpc>` prompt, you can enter commands to check the status of your printers and take other actions. |

# lpc

You can use lpc to enable or disable printers, reorder their print queues, and reexecute configuration files. To use lpc, enter the command lpc at the shell prompt. You are then given an lpc> prompt at which you can enter lpc commands to manage your printers and reorder their jobs. The status command with the name of the printer displays whether the printer is ready, how many print jobs it has, and so on. The stop and start commands can stop a printer and start it back up. The printers shown depend on the printers configured for a particular print servers. A printer configured on CUPS will only show if you have switched to CUPS. If you switch to the LPRng, those printers you configured for LPRng will show up.

```
# lpc
lpc> status myepson
myepson:
printer is on device 'parallel'
queuing is enabled
printing is enabled
1 entry in spool area
```

# lpq and lpstat

You can manage the print queue using the lpq and lprm commands. The lpq command lists the printing jobs currently on the print queue. With the -P option and the printer name, you can list the jobs for a particular printer. If you specify a username, you can list the print jobs for that user. With the -l option, lpq displays detailed information about each job. If you want information on a specific job, simply use that job's ID number with lpq. To check the status of a printer, use lpstat.

```
# lpq
myepson is ready and printing
Rank Owner Jobs File(s) Total Size
active chris 1 report 1024
```

# lprm

The lprm command enables you to remove a print job from the queue, erasing the job before it can be printed. The lprm command takes many of the same options as lpq. To remove a specific job, use lprm with the job number. To remove all printing jobs for a particular printer, use the -P option with the printer name. lprm with no options removes the job printing currently. The following command removes the first print job in the queue (use lpq to obtain the job number).

```
# lprm 1
```

# CUPS Administrative Tools

CUPS provides command line administrative tools like lpadmin, lpoptions, lpinfo, enable, disable, accept, and reject. The enable and disable commands start and stop print queues directly, whereas