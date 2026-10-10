The `stop` command has a similar effect. It will disable the printer and terminate the spooling daemon after the current job has finished.

# Disabling Print Queuing

Neither `abort` nor `stop` disables the queue. If you are taking a printer down for maintenance, for example, and you simply issue an `abort` command to kill the daemon and disable the printer, the queue will still be available. Users will be able to continue to send jobs to this printer as if nothing is wrong, and the queue will happily accept the jobs and store them to print whenever the printer becomes available. Because of this, you will probably want to disable the queue if the printer will be down for an extended period of time. There are two ways that this can be done.

The first is with the `disable` command. It requires an argument that can either be `all` to disable all queues on the system or the name of a particular printer to disable the queue for only that printer. Here’s an example:

```
```bash
lpc> disable lp
lp:

    queueing disabled

lpc> status all
lp:

    queueing is disabled
    printing is enabled
    3 entries in spool area
    waiting for lp to become ready (offline?)

lpc>
```
```

In this case, the queue is disabled, but printing is still enabled. This means that the printer will continue to print all jobs currently in the queue (if it can), but the queue will not accept any new jobs.

If you try to send a job to a printer with a down queue that is not accepting jobs, you will get an error similar to the following:

```
```bash
bash$ lpr myfile.txt
lpr: Printer queue is disabled
bash$
```
```

The other way that a queue can be disabled is by using the `down` command. Like the `disable` command, it requires at least one argument, which can either be `all` to affect all queues on the system or the name of a printer to affect only one printer.

The `down` command actually sends a `stop` command, which disables the printer and the spool daemon after the current job has finished printing, and then sends a `disable` command to bring down the queue. The `down` command can also take an optional message as an argument. The message will be written to the status file in the printer’s