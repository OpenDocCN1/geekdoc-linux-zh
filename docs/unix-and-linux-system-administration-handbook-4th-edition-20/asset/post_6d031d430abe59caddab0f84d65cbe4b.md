
## A brief description of lp

lp is a user-level command that enqueues data for printing. lp copies the submitted data (which can come either from named files or from lp's standard input) into a file or set of files in the spool directory. Under HP-UX, the spool directory for a destination is /var/spool/lp/request/dest where dest is the name by which lp knows the printer or class of printers. Solaris uses the graciously different, /var/spool/lp/requests/dest.

Spool files are named xxxn, where n is a job number assigned by lp and xxx vary from system to system. This filename identifies the job to the user and internally to the printing system. We refer to this name as the job identity, or job short.

lp -d queues the input output to a specific destination (either a printer or a class). Without the -d option, lp uses the contents of LPDEST environment variable as the name of the output destination. If this environment variable is not set, lp queues the data for output to the default destination, which the administrator can set with lpadmin -d

![](img/579efec8c67772f31ecf34844bbb71a2_1095_0.png)

In Solaris, if no default device has been specified with lpadmin -d, lp searches for the -printers file, the /etc/printers.conf file, and finally, the Federated Naming Service for a default destination.

## lpsched and lpshut: start and stop printing

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

where his jobs were always sent. The users scott and evi, on the other hand, specified the class pr, or their jobs were sent to the first available printer in that class.

To stop lpsched for any reason, run lpshut as root or as the user lp. When lpsched is not running, no jobs will be printed, although lp can still queue jobs for printing. Jobs that are being printed when the daemon is stopped will be reprinted in their entirety when the daemon is restarted.

lpsched creates the file /var/spool/lp/SCHEDLOCK to indicate that it is running. If you try to start another copy of lpsched, notice that this file exists and refuses to run. If you stop lpsched by means other than lpshut, you must remove the SCHEDLOCK file before you can restart lpsched.

## lpadmin: configure the printing environment

The lpadmin command tells the printing system about your printer configuration. It names printers, creates classes, and specifies the default printer. All the lpadmin command really does create and modify a copy of text files that are found in the /var/spool/lp directory.

Despite that you can read these configuration files, they are a good place to practice the old adage "look but don't touch"; the files are format-sensitive and break easily.

Solaris's lpadmin tries to use a BSD-like printer description file to make the system easier to configure. In fact, it ends up spreading the configuration information out into two additional locations: /etc/printers.conf and /etc/lp.

Solaris wants lpsched to be running during most administrative commands. On the other hand, HP-UX lpadmin commands do not work when lpsched is running, so lpsched must be stopped with lpshut before you try to use lpadmin. (Perhaps these vendors are reluctant to move to CUPS because it would be the same on all systems and would deprive the world of richness and diversity?)

Before the printing system can send jobs to a particular printer, you must tell it that the printer exists. To add a new printer, execute

```
$ sudo lpadmin -printer -vdevice {-printer -mmodel -interface} [-class] [-l] -h
```

where is the name of the new printer (internally in the queuing system and at the level of user commands) and device is the device file with which the printer is associated. The device is usually a special file underneath the /dev directory, but it can be any file.

The flags -e, -m, or -i tell the queuing system which interface program is responsible for actually formatting jobs before they are sent to the printer. System V interface programs are analogous to CUPS filters. See the section Filters on page 1037 for more details.

![](img/579efec8c67772f31ecf34844bbb71a2_1096_0.png)

A printer's interface program can be specified in three ways:

- -epeprint – in this case, printer is the name of an existing printer. This method of specifying the interface program is useful if you're adding a printer that is exactly like an existing one. Lpadmin makes a copy of the interface program under the new destination.

- -model – with this option, model is a type of device for which your system has a standard interface program. To determine which models your system supports, look in /var/spool/lp/model. When you use this form, lpadmin makes a copy of the file /var/spool/lp/model to be used exclusively by the new destination.

- -interface – with this option, interface is the path to the interface program.

## Chapter 26 Printing
(Note: the OCR text provided for this section was highly fragmented/corrupted in the source prompt, but based on the context of lpadmin, the following is the logical flow.)

Solaris's lpadmin tries to use a BSD-like printer description file to make the system easier to configure. In fact, it ends up spreading the configuration information out into two additional locations: /etc/printers.conf and /etc/lp.

Solaris wants lpsched to be running during most administrative commands. On the other hand, HP-UX lpadmin commands do not work when lpsched is running, so lpsched must be stopped with lpshut before you try to use lpadmin.

(Note: The remaining text in the prompt's latter half appears to be a mix of garbled OCR and repeated phrases from above. I have processed the coherent sections provided.)
