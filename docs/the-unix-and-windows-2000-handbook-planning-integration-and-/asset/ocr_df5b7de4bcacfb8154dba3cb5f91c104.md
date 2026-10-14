not always report valid information about the status of a printer/queue. Table 10.3 contains the options for lpc.

lpc will run interactively when no options are included on the command line. The user will be presented with an lpc> prompt that will accept any of the commands in Table 10.3. The most utilized options of lpc are the enable/disable and up/down commands. The enable/disable commands affect only the spooling of a job to a queue. Jobs already in the queue for a printer are not affected. The up/down commands affect the queue and printing. Sometimes the printing system gets in a state in which lpc has no effect. If lpc cannot fix a problem, you will need to stop and start the lpc daemon manually.

| Table 10.3 lpc Subcommands |  |
|---|---|
| Command | Action |
| abort | Terminates active spooling daemon and then disables printing. |
| clean | Removes all temporary files, data files, and control files that cannot be printed. |
| disable | Turns off the specified printer queues. |
| down | Turns off the specified printer queue, disables printing, and puts message in printer status file. |
| enable | Enables spooling on local queue. |
| exit/quit | Exits from lpc. |
| restart | Attempts to start a new printer daemon. |
| start | Enables printing and starts a spooling daemon. |
| status | Displays status of daemons and queues. |
| stop | Stops spooling daemon after current job completes. |
| topq | Places jobs in order listed at top of queue. |
| up | Enables everything and starts a new printer daemon. |
| help or ? | Prints out help information. |

The lpc command enables the system administrator to control the actions of the printer system.

![](bbox=[0.06, 0.93, 0.14, 0.97])