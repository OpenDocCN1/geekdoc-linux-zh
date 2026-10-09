submitted to the spooler by the `enq` command. The `enq` command is responsible for processing the job. So many of the previously listed commands are translated to the `enq` command with the proper command parameters. The `enq` command creates a job description file, or JDF, and sends notification to the `qdaemon` that a new job has been submitted.

The `qdaemon` does what you would expect: it runs at all times to manage the queues. The `qdaemon` is started at boot time from the `/etc/inittab` file. Also, the `qdaemon` is under the control of the System Resource Controller (SRC), so you can manually start, stop, and refresh the `qdaemon` at any time using the following commands:

```
```c
# startsrc -s qdaemon
# refresh -s qdaemon
# stopsrc -s qdaemon
```
```

The `qdaemon` maintains the print queues by maintaining a list of all of the defined queues and is responsible for monitoring the queues for new print jobs. When a new job is submitted, the `qdaemon` attempts to process the job if the printer resource is currently available. If the resource is not available, the job is queued and the `qdaemon` will attempt to print the job later.

The classic AIX printer subsystem has a specific flow to the queuing system. The following eight steps are followed each time a new job is submitted:

+   1.  Whichever print command is used calls the `enq` command, which checks the validity of the queue name and makes sure that the command parameters are correct. If everything passes the test, the job continues; if a problem is found, the job is rejected and the user receives an error message.

+   2.  Next the `/var/spool/lpd/qdir` directory receives an entry to identify the new print job. Some command options allow a copy of the print file to be made, which is a good idea if you want to capture a point-in-time snapshot of a file. If a copy of the source file is to be made, then the copy of the file is placed in the `/var/spool/lpd/qdaemon` directory.

+   3.  At this point, the `qdaemon` is notified that a new job exists in the `/var/spool/lpd/qdir` directory.

+   4.  When the job reaches the top of the queue, or the front of the line, the `/etc/qconf/qconf file` is read by the `qdaemon` to get a description of the queue. The `/etc/qconfig` file has a description of each queue on the system.

+   5.  When the queue starts working on the job, the `qdaemon` sends an update to the `/var/spool/lpd/stat` file showing that the job is active.

+   6.  The `backend` program for the queue is started by the `qdaemon` and receives the filename and the print options for the job, which is turned into a command-line statement.