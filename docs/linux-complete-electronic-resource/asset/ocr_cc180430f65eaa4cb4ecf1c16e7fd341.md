# ## OPTIONS AND ARGUMENTS

*-Printer* Specify the queue associated with a specific *printer* (otherwise the default *printer* is used).

* If a single `-` is given, `lprm` will remove all jobs which a user owns. If the superuser employs this flag, the spool queue will be emptied entirely.

*User* Causes `lprm` to attempt to remove any jobs queued belonging to that user (or users). This form of invoking `lprm` is useful only to the superuser.

*job #* A user may dequeue an individual job by specifying its job number. This number may be obtained from the `lqp(1)` program, e.g.:

```
% lqp -1
1st:ken [job 013ucbarpa]
(standard input) 100 bytes
% lprm 13
```

If neither arguments nor options are given, `lprm` will delete the currently active job if it is owned by the user who invoked `lprm`.

`lprm` announces the names of any files it removes and is silent if there are no jobs in the queue which match the request list.

`lprm` will kill off an active daemon, if necessary, before removing any spooling files. If a daemon is killed, a new one is automatically restarted upon completion of file removals.

# ## ENVIRONMENT

If the following environment variable exists, it is utilized by `lprm`.

*PRINTER* If the environment variable *PRINTER* exists, and a printer has not been specified with the *P* option, the default printer is assumed from *PRINTER*.

# ## FILES

+   * `/etc/printcap` Printer characteristics file.
+   * `/var/spool/*` Spooling directories.
+   * `/var/spool/*/lock` Lock file used to obtain the pid of the current daemon and the job number of the currently active job.