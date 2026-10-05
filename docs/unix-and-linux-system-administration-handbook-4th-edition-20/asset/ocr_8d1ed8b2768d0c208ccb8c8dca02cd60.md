# lpc: make administrative changes

The output lines are always in order, with the active job on top and the last job to be printed on the bottom. If the first job is listed as ist rather than active, no printing daemon is running on the printer, and you'll need to restart it.

The second column names the user who spooled each job, and the third column gives the job's identification number; this number is important to know if you intend to manipulate the job later with **lprm** or **lpc**. The fourth column gives the filenames that were listed on the **lpr** command that spooled the job. The data comes through a pipe, the entry in this column is standard input. The job size unfortunately gives no information about how many pages a job will produce or how long it will take to print.

# lprm: remove print jobs

The most common form of lprm is **lprm jobid**, where jobid is the job identification number reported by **lpq. Lpr lprm** removes all jobs belonging to user. **lprm** without arguments removes the active job. **lprm -** (that a hyphen) removes all the jobs you submitted; if you are root, it removes every job in the queue. Ordinary users cannot remove other's jobs, but the supervisor can remove any job.

Perversely, lprm fails but produces output on success. If you don't see-out that looks like this

```
dfa621xinet dequeued
cfa621xinet dequeued
```

after running lprm, it means the command failed. Either **lprm** couldn't remove the job, or you invoked the command incorrectly.

The printing system records the host on which a job originated as well the user who spooled it, and **lprm's** matching process takes both pieces of data into account. Thus garth@sig is not equivalent to garth@bouncer, and neither can remove the other's.

Trying to use the active job can cause problems on some printers. The filter process for the job may not be properly notified of the termination, with the result that the whole system comes to a grinding halt with the filter holding an exclusive lock on the port and preventing other processes from using the printer.

The only way to fix this situation is to use **ps** to identify the filter processes and to kill them by hand. **lpc** is useless in this situation. Rebooting the system always carries a cure hurt, but this is a drastic measure. Before you resort to a reboot, kill and restart the master copy of **lpd** and manually remove jobs from the spool directory with

# lpc: make administrative changes

The **lpc** command can perform the following functions:

+   * Enable or disable queuing for a particular printer
* Enable or disable printing on a particular printer