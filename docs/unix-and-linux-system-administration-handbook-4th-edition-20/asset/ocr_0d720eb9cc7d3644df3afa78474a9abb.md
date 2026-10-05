# Chapter 26 Printing

+   - Remove all jobs from a printer’s queue
- Move a job to the top of a printer’s queue
- Start, stop, restart the lpd daemon
- Get printer status information

When the printing system is running smoothly, lpc works fine. But as soon as a filter gets stuck or some minor problem appears, lpc tends to wig out completely and it lies: it sometimes fails to fix everything in reality, it has done nothing at all. You may have to fix things up by hand or power-cycle your equipment when BSD printing gets badly snarled.

lpc cannot be used across a network, so you must log into the machine that owns the printer you want to manipulate. lpc is normally used interactively, although you can also invoke it in a one-shot mode by putting one of the interactive commands on lpc’s command line. Once you have activated lpc, the various commands described below are available:

```
help [command]
```

help without arguments shows you a list of all available lpc commands. With an argument, it shows a one-line description of a particular command.

```
enable printer
disable printer
```

These commands enable or disable spooling of jobs to the named printer. Users who attempt to queue files are politely informed that spooling has been disabled. Jobs that are already in the queue are not affected.

```
start printer
stop printer
```

start enables and stop disables printing on the named printer. Print jobs can still be spooled when a printer has stopped, but they will not be printed until printing is restarted. start and stop operate by setting or clearing owner execute permission on /var/spool/lpd/printer/lock. They also start and kill the appropriate daemons for the printer. stop allows the active job to complete before printing.

```
abort printer
```

abort is just like stop, but it doesn’t allow the active job to complete. When printing is reenabled, the job will be reprinted.

```
down printer message
up printer
```

These commands affect both spooling and printing. Use them when a printer is really broken or has been taken off-line for an extended period. The message parameter supplied to down can be as long as you (on one line) and need not be quoted; it will be put in the printer’s /var/spool/lpd/printer/status file and shown to users who run lpc. You’ll normally to use this feature to register a short