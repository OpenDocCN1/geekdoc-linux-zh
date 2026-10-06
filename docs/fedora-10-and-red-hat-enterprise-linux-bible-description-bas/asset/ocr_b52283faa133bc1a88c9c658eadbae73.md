# Part III: Administering Fedora RHEL

+   Read standard input — If no command is specified, at will prompt you to enter commands at the at> prompt, as shown in the following example. You must indicate the end of the commands by pressing Ctrl+D, which signals an End of Transmission (<EOT>) to at.

```
$ at 23:40
at> cd /tmp/perl
at> make
at> ls -al
at> <Ctrl-d>
```

+   Read from file — When the -f command-line option is followed by a valid filename, the contents of that file are used as the commands to be executed, as in the following example:

```
$ -f /root/bin/runme now + 5 hours
```

This runs commands stored in /root/bin/runme in five hours. The file can be either a list of commands or a script to run in its own shell (that is, the file begins with !/bin/bash or the name of another shell).

# Viewing scheduled jobs

You can use the atq command (effectively the same as at -l) to view list of pending jobs in the queue, showing each job's number, the date and time when the job is scheduled to run, and the queue in which the job is being run.

The most common queue names are a (which represents at queue) and b (which represents the batch queue). All other letters (upper- and lowercase) can be used to specify queues with lower priority levels. The atq command lists a queue name as a =, it indicates that the job is currently running. Here is an example of output from the atq command:

```
$q
2 2008-09-02 00:51 a
3 2008-09-02 00:52 a
4 2008-09-05 23:52 a
```

Here you can see that there are three at jobs (job numbers 2, 3, and 4, all indicated as a). After the job number, the output shows the date and hour each job is scheduled to run.

# Deleting scheduled jobs

If you decide to cancel a particular job, you can use the atm command (equivalent to at -d) with the job number (or more than one) as reported by the atq command. For example, using the following output from atq:

```
$ atq
18 2008-09-01 03:00 a
19 2008-09-29 05:27 a
```