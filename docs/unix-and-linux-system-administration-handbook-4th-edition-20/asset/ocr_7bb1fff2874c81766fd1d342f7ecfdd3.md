# A brief description of lp

lp is a user-level command that enqueues data for printing. lp copies the submitted data (which can come either from named files or from lp's standard input) into a file or set of files in the spool directory. Under HP-UX, the spool directory for a destination is /var/spool/lp/request/dest where dest is the name by which lp knows the printer or class of printers. Solaris uses the graciously different, /var/spool/lp/requests/dest.

Spool files are named xxxn, where n is a job number assigned by lp and xxx vary from system to system. This filename identifies the job to the user and internally to the printing system. We refer to this name as the job identity, or job short.

lp -d queues the input output to a specific destination (either a printer or a class). Without the -d option, lp uses the contents of LPDEST environment variable as the name of the output destination. If this environment variable is not set, lp queues the data for output to the default destination, which the administrator can set with lpadmin -d

![](bbox=[0.145, 0.443, 0.235, 0.473])

In Solaris, if no default device has been specified with lpadmin -d, lp searches for the -printers file, the /etc/printers.conf file, and finally, the Federated Naming Service for a default destination.

# lpsched and lpshut: start and stop printing

The lpsched daemon sends files placed in the spool directory by lp to an appropriate daemon as soon as one is available. lpsched keeps a log of each file it processes and of any errors that occur.

In Solaris, the default log file is /var/lp/logs/lpsched. HP-UX keeps the log file in /var/adm/lp/log; when lpsched starts (normally at boot time), it moves the old log to oldlog and starts a new one.

A log file looks like this: *****

| LP LOG: Jun 6 12:05 ***** |
| pr-107 garth pr1 Jul 6 12:10 |
| pr-112 scott pr1 Jul 6 12:22 |
| pr-117 evi pr2 Jul 6 12:22 |
| pr-118 garth pr1 Jun 6 12:25 |
| pr-119 garth pr1 Jun 6 13:38 |
| pr-132 evi pr1 Jul 6 13:42 |

The first column is the jobid of each job. The second column is the user who requested the job. The third column is the actual printer the job was sent to, and the last column is the time at which the job was queued.

The HP-UX system in this example lists two printers: pr1 and pr2, both of which are in the class pr. The user g always specified the specific printer pr1, so that's