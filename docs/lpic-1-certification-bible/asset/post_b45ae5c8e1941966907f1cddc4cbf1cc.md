
## Using lpr

The `lpr` command syntax is as follows:

```
lpr [ -A ] [ -b ] [ -C class ] [ -D debugopt ]
     [ -F filterformat ] [ -h ] [ -i indentscols ]
     [ -k ] [ -J job ] [ -K # copies ]
     [ -m mailTo ] [ -P printer ] [ -Q ] [ -r ]
     [ -R remoteAccount ] [ -s ] [ -T title ] [ -U user ]
     [ -V ] [ -w width ] [ -Z zoptions ] [ -1,2,3,4 font ]
     [ filename... ]
```

| Option | Function |
| :--- | :--- |
| -A | Uses the authentication type specified in the AUTH environment variable. |
| -C <class> | Specifies the job priority, which ranges from A (slowest) to Z (fastest). The default is A. |
| -D <debug options> | Specifies options to enable debugging mode. See the lpr man page for more information. |
| -F <filter format> | Specifies a filter or format specification instead of the default filter. |
| -h | Indicates no banner page for this job. |
| -i <indent columns> | Indents the job the specified number of columns. |
| -J <job name> | Specifies the job name. |
| -k | Sends the print job directly to the server, instead of waiting for the full job to go through the filter. |
| -K <copies> , -# <copies> | Prints the specified number of copies. |
| -m <mail to> | Sends mail to the specified address if the job does not complete successfully. |
| -P <printer> | Specifies the destination printer instead of using the default. |
| -Q | Puts the name of the spool queue in to the job file. This is sometimes used with other spooling software. |
| -R <remote account> | Specifies accounting information for the remote system. |
| -s | Creates a symbolic link to the file to be printed instead of sending the file directly. This is supported for backward compatibility. |
| -T <title> | Specifies the title name. |
| -U <user name> | Allows root to change the username associated with a job. |
| -V | Enables verbose mode. Multiple `-V` parameters can be added to increase output. |
| -W <width> | Specifies the page width for the job. |
| -Z <options> | Allows you to pass special options directly to the print spooler. |

For example, to print the /etc/hosts file to the printer named hp1j with lpr you would type the following:

```
[root@redhat /root]# lpr -Php1j /etc/hosts
```

## Using a2ps

Many sites that use UNIX systems have PostScript printers, since this is considered to be the standard printing language to use. But, if you send a text file directly to a PostScript printer, it will not print correctly. To change the format you can use the a2ps tool, which ships with many distributions. To convert the file myfile.txt to PostScript, you would type the following:

```
a2ps -o myfile.ps myfile.txt
```

The -o option specifies the output file name. To print a text file to the default printer as PostScript you would type the following:

```
a2ps myfile.txt
```

# Troubleshooting Printing Problems

Troubleshooting printing problems can be confusing because of the different pieces involved. A messed-up queue, crashed lpd, or jammed printer all result in the same problem, no printing. The tools are available to help narrow down and find the problem.

## lpd problems

If no printers are working, the first thing to check is the lpd daemon. A quick process list check will show if it is still loaded. For example:

```
[root@redhat /root]# ps auxw | grep lpd
lp        14743  0.0  0.0  2432  192 ?     S    Jan03   0:00
lpd Waiting
```

Another option is to check the startup script. For example, if you checked the script and the `lpd` daemon had crashed you would see this:

```
[root@redhat /root]# /etc/rc.d/init.d/lpd status
lpd dead but subsys locked
```

A simple restart command should fix the problem. For example:

```
[root@redhat /root]# /etc/rc.d/init.d/lpd restart
Stopping lpd:                                   [FAILED]
Starting lpd:                                  [  OK  ]
```

If the `lpd` daemon has crashed, be sure to check the syslog for possible information.

## Queue problems

If print jobs seem to be stalled in the print queue, make sure the queue has not been disabled. This can be checked with the `lpc` command. For example:

```
debian:~# lpc status
lp:
         queuing is enabled
         printing is enabled
         no entries
         no daemon present
```

An example of the command using LPRng is as follows:

```
[root@redhat /root]# lpc status all
         Printer Printing Jobs Server Subserver Redirect
Status/(Debug) enabled disabled 0 none none (hold)
```

Notice that the spooling service has been disabled. To enable it use the following command:

```
debian:~# lpc enable all
lp:
        queuing enabled
```

An example of the command using LPRng is as follows:

```
[root@redhat /root]# lpc enable all
Printer: lp@redhat
lp@redhat.the-nashes.net: enabled
```

```
[root@redhat /root]# lpc status
Printer      Printing Spooling Jobs  Server Subserver Redirect
Status/(Debug)
lpc@redhat        enabled enabled    0    none     none      (hold)
```

## Printer problems

The printer itself may also be a problem. First, make sure printing has not been disabled on this printer. This can be checked with `lpc`. For example:

```
debian:~# lpc status
lp:
     queuing is enabled
     printing is enabled
     no entries
     no daemon present
```

An example of this command with LPRng would be as follows:

```
[root@redhat /root]# lpc status
Printer      Printing Spooling Jobs  Server Subserver Redirect
Status/(Debug)
lpc@redhat        disabled disabled    0    none     none      (hold)
```

Notice that printing has been disabled on this device. Printing can be turned back on using the `up` command, for example:

```
debian:~# lpc up all
lp:
     printing enabled
daemon started
```

An example of the command using LPRng is as follows:

```
[root@redhat /root]# lpc up all
Printer: lpc@redhat
lpc@redhat:the-nashes.net: enabled and started
```

If printing is enabled and still no jobs are getting processed, you may need to check the actual printer. Make sure it is turned on and has paper in it. A quick way to check the printing hardware is to `cat` a file to the printer interface. For example, to check a printer attached to the system’s parallel port you would use the following:

```
[root@redhat /root]# cat /etc/host > /dev/lpt0
```

This dumps the text file directly to the hardware interface, bypassing the LPD system.

## File and directory problems

Usually the *printcap* file is not the problem, unless this is the first time the printer has been used. Make sure that the first line in a printer block does not start with a colon or pipe. Make sure all lines except the last one in the block end in `:`. If multiple printers are configured, make sure they have separate spool directories.

Check the printer definitions so the interface device or remote system is correct, and a very small maximum print job size is not set. If you configured the file manually, you may try one of the configuration tools such as Apsfilter or PrintTool.

The next step is to look at the spool directory, ownership, and permissions. If a configuration tool made these for you, they are most likely correct, but should be checked anyway. Make sure the proper ownership was granted and the permissions are correct, or the *lpd* daemon will not be able to create files there.

## Space problems

If your system runs out of disk space new spool files cannot be created. Check the disk space on the volume containing */var* and make sure adequate space is available.

## Key Point Summary

The Linux printing system can be complex to the uninitiated, but the key lies in knowing where to go for information. The different tools sometimes seem to overlap, but provide the ability to troubleshoot and debug almost any problem.

- Most Linux distributions use the LPR printing system.
- Local and remote printer configuration is stored in the */etc/printcap* file.
- Printer blocks in the */etc/printcap* begin with a line specifying the printer name and optional aliases.
- Printer configuration definitions begin with a colon.
- All lines in the */etc/printcap* file end in `:`, except for the last one in a printer block.
- The print spool directory and log file must be created manually.
- Print access is controlled with the */etc/hosts.lpd* file.
- Print filters format different data types to a language understood by the printer.
