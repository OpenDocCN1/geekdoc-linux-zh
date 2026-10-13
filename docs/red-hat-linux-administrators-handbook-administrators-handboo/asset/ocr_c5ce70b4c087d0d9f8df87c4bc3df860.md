# Scheduling Processes

Like all other forms of UNIX and UNIX-like OSs, Red Hat Linux provides you with two widely used process scheduling facilities. This section describes how to use both of these services.

# Using at

The at utility allows you to queue a command for execution at a later time. For example, to run the disk usage summary generator utility called du at 8:40 p.m., you can run at as follows:

```
at 20:40
```

The at command displays a prompt such as at>, where you can enter the du command as follows:

```
at> du -a > /tmp/du.out
```

Here, the output of du is directed to a file. After you enter the command (the du command, in this example), at displays the prompt again. You can press Ctrl+D to exit. You will see a message similar to the one here:

```
at> <EOT>
warning: commands will be executed using /bin/sh
job 1 at 1999-12-06 20:40
```

This means that at has scheduled the du -a > /tmp/du.out job to be run by the at daemon (atd) at 8:40 p.m., 12/06/1999. You can use a wide variety of time formats to specify the time of execution. For example, instead of saying at 20:40, you can say at 8:40pm, as well. You can also specify the date along with the time. For example, 8:40pm feb 23, 10am + 5 days, 12:30pm tomorrow, midnight, and noon are all valid time specifications.

To verify that your job is in the job queue, run the atq command, which shows the currently scheduled jobs in the queue. All the scheduled jobs are stored in the /var/spool/at directory.